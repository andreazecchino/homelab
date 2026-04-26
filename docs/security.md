# Security Setup

## Secret encryption at rest

Encryption at rest has been enabled at server first startup by passing the flag `--secrets-encryption` to the installation script. This means that secrets are encrypted in the etcd database rather than stored as plaintext and remain protected if someone gain access to the etcd storage.

## Secrets Management

I chose Sealed Secrets to enable GitOps workflows with secrets in version control. It uses a Custom Resource Definition, allowing you to manage encrypted secrets with the same `kubectl` commands and workflows as regular Kubernetes manifests. Sealed secrets can be safely committed to Git repositories since only the cluster's sealing key can decrypt them, keeping the encryption key secure within the cluster.

