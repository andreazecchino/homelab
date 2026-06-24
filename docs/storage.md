# Storage

## Longhorn

Longhorn is a lightweight, open-source distributed block storage system built for Kubernetes using CRDs and CSI integration. It runs on commodity hardware using nodes storage capacity without requiring external infrastructure. It provides built-in snapshots, incremental backups and automatic volume replication across nodes for high availability and disaster recovery. Longhorn was chosen over the `local-path` StorageClass to provide high availability and overcome the limitations of node-local storage.

The Longhorn deployment is optimized for small Kubernetes clusters on commodity hardware with limited resources. It balances high availability with resource efficiency by configuring replicas and CSI components to 1, reducing overhead while maintaining distributed storage capabilities.
