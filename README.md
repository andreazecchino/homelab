# Homelab

This is the place where I began my journey with Kubernetes.

## Introduction

The scope of this project is to build a Kubernetes cluster with [K3s](https://k3s.io), learn to deploy applications and automate its deployment and configuration applying **IaC** and **GitOps** methodologies.

## Hardware

Currently the cluster is running on:

| Node | Role | Hardware |
| ---- | ---- | -------- |
| Raspberry Pi 4 | Control Plane | 4GB RAM, 64GB microSD |
| Raspberry Pi 4 | Worker Node | 4GB RAM, 64GB microSD |

At the moment it isn't reachable from the Internet.

## Technology Stack

**Operating System**:

- **[Raspberry Pi OS](https://www.raspberrypi.com/software/)**: Raspberry Pi official operating system

**Automation**:

- **[Cloud-init](https://cloud-init.io)**: Open source tool for automatically initializing and customizing an instance of a Linux distribution
- **[FluxCD](https://fluxcd.io)**: GitOps tool to automate the deployment and lifecycle management of applications and infrastructure on Kubernetes

**Kubernetes Distribution**:

- **[K3s](https://k3s.io)**: Lightweight Kubernetes distribution (with default settings)

**Management**:

- **[K9s](https://github.com/derailed/k9s)**: Terminal-based UI for managing Kubernetes clusters

**Observability**

- **[Prometheus](https://prometheus.io)**: An open-source monitoring and alerting toolkit
- **[Grafana](https://grafana.com)**: Web application for monitoring data


## End User Applications

| Name | Description |
| ---- | ----------- |
| [Commafeed](https://www.commafeed.com) | A self-hosted RSS feed reader inspired by Google Reader |

