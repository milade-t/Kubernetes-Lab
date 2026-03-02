# Kubernetes-Lab
Kubernetes Cluster (Control Plane + Worker)
# Kubernetes Cluster Bootstrap (kubeadm)

Debian / Ubuntu · containerd · Flannel · NodePort

Kubernetes Cluster Bootstrap is a documented workflow for deploying a Kubernetes cluster using kubeadm.

This repository describes how to provision:

- A single control plane node
- A worker node
- containerd as the container runtime
- Flannel (VXLAN) as the CNI
- NodePort for service exposure

The focus is on reproducibility, validation, and operational clarity.

This project does not aim to abstract or automate cluster creation. It documents the exact steps required to bootstrap, validate, and troubleshoot a kubeadm-based deployment.

---

## Architecture

The cluster consists of:

- 1 Control Plane node
- 1 Worker node
- kube-proxy (iptables mode)
- Flannel networking
- Static pod–managed control plane components

Pod CIDR: `10.244.0.0/16`  
Service CIDR: `10.96.0.0/12`

---

## Purpose

This repository exists to:

- Provide a clean reference for kubeadm cluster setup
- Document required kernel, networking, and runtime configuration
- Capture validation steps before and after initialization
- Describe common failure states and recovery procedures
- Serve as the foundation for future automation

---

## Documentation

- Architecture
- Environment requirements
- Control plane bootstrap
- Worker node join
- Cluster verification
- Networking model
- Service exposure (NodePort)
- Troubleshooting
- Reset and cleanup

All commands are tested against:

- Debian 13
- Ubuntu 22.04 LTS
- Kubernetes v1.34.x

---

## Getting Started

Review the documentation under `docs/` and begin with:

`02-environment-requirements.md`

---

## Scope

This repository covers:

- kubeadm-based deployments
- Single control plane topology
- Lab and development environments

It does not cover:

- High availability control planes
- External etcd clusters
- Managed Kubernetes services
- Production hardening

---

## Contributing

This repository is documentation-driven.  
Improvements to clarity, validation steps, or troubleshooting coverage are welcome.

---

## License

MIT
