# Networking

## Cilium

Cilium is an open source, cloud native solution for providing, securing, and observing network connectivity between workloads. Unlike `kube-proxy`, which relies on iptables, Cilium uses eBPF (extended Berkeley Packet Filter) for efficient kernel-level networking, reducing overhead compared to traditional iptables-based CNIs. 

It also offers advanced security and policies enforcement by:

- enforcing identity-aware policies based on Kubernetes labels (beyond standard L3/L4 controls)
- enabling fine-grained control over specific application requests with L7 policies (HTTP paths, DNS names, etc.)
- transparent encryption

Cilium is perfect for experimenting with advanced networking concepts and understanding modern cloud-native networking.
