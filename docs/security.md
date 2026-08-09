# Security Setup

## Secret encryption at rest

Encryption at rest has been enabled at server first startup by passing the flag `--secrets-encryption` to the installation script. This means that secrets are encrypted in the etcd database rather than stored as plaintext and remain protected if someone gain access to the etcd storage.

## Secrets Management

I chose Sealed Secrets to enable GitOps workflows with secrets in version control. It uses a Custom Resource Definition, allowing you to manage encrypted secrets with the same `kubectl` commands and workflows as regular Kubernetes manifests. Sealed secrets can be safely committed to Git repositories since only the cluster's sealing key can decrypt them, keeping the encryption key secure within the cluster.

## Container hardening

I demonstrate Kubernetes security best practices through hardened application manifests designed for production environments. Where applicable, my security implementations include:

- `drop: ["ALL"]` to eliminate unnecessary Linux capabilities
- `allowPrivilegeEscalation: false` to prevent privilege escalation attacks
- `runAsNonRoot: true` and `runAsUser: 1000` to enforce non-root container execution

## Certificate management

For certificate management, I relied on a local CA. The following steps establish a Root CA and integrate it within the cluster.

- Create the CA's private key: `openssl genrsa -out MyLocalCA.key 4096`
- Generate the CA certificate with a 10-year validity period: `openssl req -x509 -new -nodes -key MyLocalCA.key -sha256 -days 3650 -out MyLocalCA.pem`
- Make the CA certificate trusted by the nodes' operating system (in this case Ubuntu Server):
  - `sudo cp MyLocalCA.pem /usr/local/share/ca-certificates/MyLocalCA.crt`
  - `sudo update-ca-certificates`
  - the same step must be done on development machine based on its operating system
- Add the cluster's IP addresses and DNS names to the development machine's `/etc/hosts` file to enable local DNS resolution without external lookups

Store the CA certificate and key in a Kubernetes Secret:

```bash
kubectl create secret tls ca-key-pair \
  --cert=MyLocalCA.pem \
  --key=MyLocalCA.key \
  --namespace=<namespace> \
  --dry-run=client \
  -o yaml > secret.yaml
```

Encrypt the secret using `kubeseal` as described in the [quick setup](quicksetup.md) guide.
