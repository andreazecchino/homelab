# Homelab

Configurations and documentation of my homelab.

## Introduction

This is the place where I began my journey with Kubernetes, with testing and tinkering.

## Hardware

Currently the cluster is running on:

| Node | Role | Hardware |
| ---- | ---- | -------- |
| Raspberry Pi 4 | Control Plane | 4GB RAM, 64GB microSD |
| Raspberry Pi 4 | Worker Node | 4GB RAM, 64GB microSD |

At the moment it isn't reachable from the Internet.

## Tech Stack

| Category | Name | Description |
| ---- | ---- | ----------- |
| OS | [Raspberry Pi OS](https://www.raspberrypi.com/software/) | Raspberry Pi official operating system |
| Automation | [Cloud-init](https://cloud-init.io) | Open source tool for automatically initializing and customizing an instance of a Linux distribution  |
| Automation | [FluxCD](https://fluxcd.io) | GitOps tool to keep Kubernetes cluster in sync with sources of configuration |
| Kubernetes | [K3s](https://k3s.io) | Lightweight Kubernetes distribution (with default settings) |
| Management | [K9s](https://github.com/derailed/k9s) | Terminal-based UI for managing Kubernetes clusters |

## Apps

| Name | Description |
| ---- | ----------- |
| [Commafeed](https://www.commafeed.com) | A self-hosted RSS feed reader inspired by Google Reader |

