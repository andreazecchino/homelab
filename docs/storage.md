# Storage

## Longhorn

Longhorn is a lightweight, open-source distributed block storage system built for Kubernetes using CRDs and CSI integration. It runs on commodity hardware using nodes storage capacity without requiring external infrastructure. It provides built-in snapshots, incremental backups and automatic volume replication across nodes for high availability and disaster recovery. The high availability is the main reason why I chose it over `local-path` StorageClass.
