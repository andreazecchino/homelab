# Overview

This documentation covers the setup and management of a Kubernetes homelab running on Raspberry Pi hardware. The cluster is powered by **K3s**, **FluxCD** and **GitOps** principles and it's designed for experimentation and learning, with a focus on simplicity and resource efficiency. All operations prioritize command-line tooling, providing a lightweight and efficient management experience.

Key characteristics:

- **Lightweight**: K3s runs efficiently on constrained hardware with minimal resource overhead
- **Declarative**: All cluster state is defined in Git and automatically reconciled by FluxCD
- **Reproducible**: Configuration as code ensures consistent deployments
- **Auditable**: Git history provides a complete audit trail of all cluster changes
- **CLI-First**: All management tasks use command-line tools for efficiency and scriptability

## Why K3s?

**K3s** is a certified Kubernetes distribution that reduces the dependencies and steps required to build a Kubernetes cluster without compromising core functionality. Specifically designed to run on low-resource hardware, it's a good choice to leverage existing **Raspberry Pi** hardware. 

**Raspberry Pi OS Lite** is used as the base operating system. This is the officially supported and recommended OS for Raspberry Pi, ensuring optimal compatibility and hardware utilization.

Aligning with the CLI-first approach, **K9s** is the primary management tool for the cluster, providing a command-line user interface (TUI) for real-time cluster monitoring and debugging.

## GitOps with FluxCD

**GitOps** is an operational model where Git repositories serve as the single source of truth for declarative infrastructure and applications. Instead of manually running commands or using deployment tools, you commit configuration changes to Git, and automated systems reconcile the cluster to match.

**FluxCD** is the GitOps operator chosen for this Kubernetes homelab (following the CLI-first approach), with a monorepo repository structure. The reconciliation model is Pull-based (Flux continuously pulls configuration from Git) which grants no exposure to external systems and works even if the cluster is behind NAT or firewalls.

