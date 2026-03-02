01 — System Requirements

This guide assumes a clean Linux machine with no Kubernetes components installed.

1. Operating System

Install one of:

Ubuntu 22.04 LTS (recommended)

Debian 12+

Check:

cat /etc/os-release
2. Hardware (Per Node)

Minimum:

2 CPU

4GB RAM

30GB Disk

Recommended:

2–4 CPU

8GB RAM

40GB Disk

Check CPU:

nproc

Check memory:

free -h

Check disk:

df -h

Ensure at least 20GB free before starting.

3. Unique Hostname

Each node must have a unique hostname.

Check:

hostnamectl

Set if needed:

sudo hostnamectl set-hostname control-plane

(or worker for worker node)

4. Network Connectivity

Nodes must be able to reach each other via IP.

Test:

ping <other-node-ip>

Control plane must later expose port 6443.

5. Clean System Requirement

Machine must NOT have:

Docker installed

snap Kubernetes packages

Previous kubeadm cluster

Old CNI configuration

Check for existing Kubernetes directories:

ls /etc/kubernetes

If directory exists and this is not a new install, perform reset before continuing.

6. Swap Must Be Disabled

Check:

swapon --show

If swap is enabled, it will be disabled in the next phase.

Pre-Deployment Checklist

 Clean OS installed

 Minimum hardware satisfied

 Unique hostname configured

 Network connectivity verified

 No previous Kubernetes installation

If all checks pass, proceed to:

02-linux-preparation.md
