# Kubernetes Cluster Bootstrap (kubeadm)

![release](https://img.shields.io/badge/release-v0.2.0-blue)
![kubernetes](https://img.shields.io/badge/kubernetes-v1.34.x-326ce5)
![runtime](https://img.shields.io/badge/runtime-containerd-575757)
![cni](https://img.shields.io/badge/network-Flannel-blue)
![docs](https://img.shields.io/badge/status-operational--guide-green)
![license](https://img.shields.io/badge/license-MIT-green)

Debian / Ubuntu · containerd · Flannel · NodePort

---

## Overview

Kubernetes Cluster Bootstrap is a structured, step-by-step operational guide for deploying a Kubernetes cluster using `kubeadm`.

This repository documents how to provision:

- A single control plane node
- A worker node
- containerd as the container runtime
- Flannel (VXLAN) as the CNI
- NodePort for service exposure

The focus is reproducibility, validation, and operational clarity.

This project does not automate cluster creation.  
It documents the exact procedures required to bootstrap, validate, and troubleshoot a kubeadm-based deployment.

---

## Architecture

<img width="1536" height="1024" alt="ChatGPT Image Mar 3, 2026, 08_30_24 AM" src="https://github.com/user-attachments/assets/2e934e54-4035-4c36-89e3-cbbc829dff8e" />


Topology:

- 1 Control Plane node
- 1 Worker node
- Static pod–managed control plane components
- kube-proxy (iptables mode)
- Flannel overlay networking (VXLAN)

Cluster configuration:

- Pod CIDR: `10.244.0.0/16`
- Service CIDR: `10.96.0.0/12`

---

## Documentation Structure

The full deployment workflow is organized under `docs/`:

1. `01-system-requirements.md`
2. `02-linux-preparation.md`
3. `03-runtime-installation.md`
4. `04-kubernetes-installation.md`
5. `05-preflight-validation.md`
6. `06-control-plane-init.md`
7. `07-install-cni.md`
8. `08-worker-join.md`
9. `09-post-install-validation.md`

The guide is intentionally linear and should be followed in order.

---

## Tested Environment

All commands validated on:

- Debian 13
- Ubuntu 22.04 LTS
- Kubernetes v1.34.x
- containerd 1.7.x
- Flannel (latest stable)

---

## Getting Started

Begin here:

👉 `docs/01-system-requirements.md`

Follow each section sequentially.

---

## Scope

This repository covers:

- kubeadm-based deployments
- Single control plane topology
- Lab and development environments
- Manual validation and troubleshooting

This repository does **not** cover:

- High availability control planes
- External etcd clusters
- Managed Kubernetes services (EKS, AKS, GKE)
- Production hardening or security benchmarks

---

## Design Principles

- Prescriptive and command-driven
- Minimal narrative
- Validation after every phase
- Explicit failure recovery steps

---

## Contributing

This repository is documentation-driven.  
Improvements to clarity, validation accuracy, or operational coverage are welcome.

---

## License

MIT
