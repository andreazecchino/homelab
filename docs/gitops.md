# GitOps with FluxCD

**GitOps** is an operational model where Git repositories serve as the single source of truth for declarative infrastructure and applications. Instead of manually running commands or using deployment tools, you commit configuration changes to Git, and automated systems reconcile the cluster to match.

**FluxCD** is the GitOps operator chosen for this Kubernetes homelab (following the CLI-first approach), with a monorepo repository structure. It uses a pull-based reconciliation model where the cluster continuously pulls configuration from Git, which eliminates the need for external webhooks or inbound access to the cluster.
