# Storage

## Longhorn

Longhorn is a lightweight, open-source distributed block storage system built for Kubernetes using CRDs and CSI integration. It runs on commodity hardware using nodes storage capacity without requiring external infrastructure. It provides built-in snapshots, incremental backups and automatic volume replication across nodes for high availability and disaster recovery. Longhorn was chosen over the `local-path` StorageClass to provide high availability and overcome the limitations of node-local storage.

The Longhorn deployment is optimized for small Kubernetes clusters on commodity hardware with limited resources. It balances high availability with resource efficiency by configuring replicas and CSI components to 1, reducing overhead while maintaining distributed storage capabilities.

### Multi-Attach Volume Errors

With `ReadWriteOnce` volumes, I choose the `Recreate` deployment strategy to prevent conflicts. `ReadWriteOnce` volumes can only attach to one pod at a time. `RollingUpdate` deployments start new pods before terminating old ones, which causes the new pods to fail when attempting to attach the same volume. `Recreate` solves this by terminating all existing pods first, ensuring the volume is fully released before new pods attempt to attach it.

## CloudNativePG

CloudNativePG is a Kubernetes operator for PostgreSQL. It exposes native CRDs for declarative cluster management and includes features such as automated failover and backup management.

I chose this operator as the storage solution for the applications because it simplifies database lifecycle management alongside application deployments, but resource constraints force me to drop some functionality and heavily tune database parameters. The settings tune PostgreSQL for a low‑memory, low‑I/O environment: fewer checkpoints, smaller memory allocations, and trade‑offs between durability and throughput to reduce disk and memory pressure.
