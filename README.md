# Homelab

This repository contains all the documentation and configuration of my Kubernetes homelab powered by [K3s](https://k3s.io).

## Introduction

The primary goal of this project is to build a Kubernetes cluster, learn to deploy applications and automate configuration using **GitOps** methodologies. Additionally, I plan to self-host some applications for personal use.

For additional informations:

- [Overview](docs/overview.md)
  - [GitOps](docs/gitops.md)
  - [Security](docs/security.md)
  - [Storage](docs/storage.md)
  - [Networking](docs/networking.md)

## Hardware

Currently the cluster is running on:

| Node | Role | Hardware |
| ---- | ---- | -------- |
| Raspberry Pi 4 | Control Plane | 4GB RAM, 64GB microSD (OS) + 256GB USB Flash Drive (Longhorn) |
| Raspberry Pi 4 | Worker Node | 4GB RAM, 64GB microSD (OS) + 256GB USB Flash Drive (Longhorn) |

At the moment it isn't reachable from the Internet.

## Technology Stack

- [Ubuntu Server](https://ubuntu.com/download/raspberry-pi): OS flavor for Raspberry Pi
- [K3s](https://k3s.io): Lightweight Kubernetes distribution for resource-retrained, remote or IoT environments
- [K9s](https://github.com/derailed/k9s): Terminal-based UI for managing Kubernetes clusters
- [Cloud-init](https://cloud-init.io): Open source tool for automatically initializing and customizing an instance of a Linux distribution
- [FluxCD](https://fluxcd.io): GitOps tool to automate the deployment and lifecycle management of applications and infrastructure on Kubernetes
- [Longhorn](https://longhorn.io/): Distributed block storage system for Kubernetes
- [Prometheus](https://prometheus.io): Open source metrics collection and alerting system
- [Grafana](https://grafana.com): Web-based visualization and dashboarding platform for querying and displaying metrics
- [Cert-manager](https://cert-manager.io/): Open source, cloud native certificate management controller
- [Cilium](https://cilium.io/): Open source networking, security and observability solution utilizing eBPF technology


## Deployed Applications

- [Commafeed](https://www.commafeed.com): a self-hosted RSS feed reader inspired by Google Reader
