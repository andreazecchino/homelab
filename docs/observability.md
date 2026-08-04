# Observability

## kube-prometheus-stack 

For observability, I relied on a comprehensive Helm chart that bundles **Prometheus** (for metrics collection), **Grafana** (for data visualization), **Alertmanager** (for alert routing), and related components into a production-ready monitoring solution for Kubernetes. By using Kubernetes-native pattern, you manage monitoring the same way you manage other Kubernetes resources, making it GitOps-friendly. The modular design lets you enable or disable components and customize configurations with ease. With the pre-built dashboards, you gain visibility immediately without starting from scratch.

I also attempted to integrate **Alloy**, **Loki**, and **Tempo** for enhanced observability, but disabled them due to hardware constraints - microSD and USB flash drives lack the performance and reliability these components require. NVMe disks or remote storage would be better suited.
