# Homelab

Configurations and documentation of my homelab.

## Introduction

This is the place where I began my journey with Kubernetes, with testing and tinkering.

## Hardware

Currently the cluster is running on:

| Node | Role | Hardware | OS |
| ---- | ---- | -------- | -- |
| Raspberry Pi 4 | Control Plane | 4GB RAM, 64GB microSD | Raspberry Pi OS 64-bit |
| Raspberry Pi 2 | Worker Node | 1GB RAM, 16GB microSD | Raspberry Pi OS 32-bit |

With [K3s](https://k3s.io/) as Kubernetes distribution (with default settings).

I'm using [K9s](https://github.com/derailed/k9s) to manage the cluster.
