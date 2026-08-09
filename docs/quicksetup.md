# Quick setup

## Nodes system setup

```bash
# Essential packages for Longhorn storage
sudo apt update && sudo apt install -y \
  open-iscsi \
  nfs-common 

# Enable and start iSCSI (required for Longhorn)
sudo systemctl enable --now iscsid

# Longhorn Volume Mount Issues, check if multipathd is running
sudo systemctl status multipathd

# Disable multipath daemon on all nodes
sudo systemctl disable --now multipathd
sudo systemctl is-active multipathd
```

## K3s master node setup

```bash
# On Master node, run:
export MASTER_IP=192.168.178.40 # customize it
curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION="v1.35.1+k3s1" \
  INSTALL_K3S_EXEC="server \
  --node-ip $MASTER_IP \
  --secrets-encryption \
  --disable=flannel,local-storage,metrics-server,servicelb,traefik \
  --flannel-backend=none \
  --disable-network-policy \
  --disable-cloud-controller \
  --disable-kube-proxy" sh -s -

# Get the token on Master node
sudo cat /var/lib/rancher/k3s/server/node-token

# Configure kubectl access (on your development machine)
mkdir -p $HOME/.kube
sudo rsync -avp <master-user>@<master-ip>:/etc/rancher/k3s/k3s.yaml $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config && chmod 600 $HOME/.kube/config
```

## K3s worker node setup

```bash
# On Worker node(s), run:
export MASTER_IP=192.168.178.40 # customize it
export K3S_TOKEN=your-node-token
curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION="v1.35.1+k3s1" \
  K3S_URL=https://$MASTER_IP:6443 \
  K3S_TOKEN=$K3S_TOKEN sh -
```

## System setup

Install the following software on your development machine using a package manager or installation scripts:

- kubectl
- Cilium CLI
- Flux CLI
- kubeseal

Verify the nodes: `kubectl get nodes -o wide`

## Cilium setup

```bash
# Gateway API CRDs installation
kubectl apply -f https://github.com/kubernetes-sigs/gateway-api/releases/download/v1.4.1/standard-install.yaml

# Cilium installation
cilium install --version 1.19.5 \
  --set kubeProxyReplacement=true \
  --set gatewayAPI.enabled=true
cilium status --wait # Validate installation
# Identify the correct network interface on master node before apply the CiliumL2AnnouncementPolicy
```

## FluxCD setup

```bash
# Flux pre-installation check
export GITHUB_TOKEN=<token> # PAT with Administration (RW), Contents (RW) and Metadata (RO) permissions
export GITHUB_USER=<username>
flux check --pre
# Flux GitHub bootstrap
flux bootstrap github \
  --owner=$GITHUB_USER \
  --repository=homelab \
  --branch=main \
  --path=./clusters/staging \
  --personal
```

## Sealed Secrets restore or setup

```bash
# Apply sealed-secrets private keys and restart the controller pod
kubectl apply -f private.key
kubectl delete pod -n kube-system -l name=sealed-secrets-controller

# Or recreate all SealedSecret objects:
# Make a backup of the encryption keys:
kubectl get secret -n kube-system -l sealedsecrets.bitnami.com/sealed-secrets-key -o yaml > private.key
# Retrieve the public key
kubeseal --fetch-cert \
  --controller-name=sealed-secrets-controller \
  --controller-namespace=flux-system > pub-sealed-secrets.pem
# Generate a single Kubernetes secret manifest with kubectl
kubectl -n <namespace> create secret generic basic-auth \
  --from-literal=user=admin \
  --from-literal=password=change-me \
  --dry-run=client \
  -o yaml > secret.yaml
# Encrypt the secret with kubeseal
kubeseal --format=yaml --cert=pub-sealed-secrets.pem \
  < secret.yaml > secret-sealed.yaml
# Delete the plain secret and apply the sealed one:
rm secret.yaml
kubectl apply -f secret-sealed.yaml
# Repeat for all other secrets
```
