05 — Preflight Validation (Control Plane)

Perform these checks on the control plane node before initializing the cluster.

1. Confirm containerd Is Running
sudo systemctl status containerd

Expected:

active (running)
2. Confirm kubelet Is Enabled
sudo systemctl status kubelet

Note: kubelet may show errors before initialization.
This is normal.

3. Confirm Swap Is Disabled
swapon --show

No output should appear.

4. Run kubeadm Preflight Dry-Run
sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --dry-run

Expected:

No fatal errors

Preflight checks pass

If errors occur:

Common causes:

Swap enabled

Ports already in use

Old cluster state

container runtime not detected

5. If Reinitializing (Cleanup)

If this node was previously used for Kubernetes:

sudo kubeadm reset -f

Remove residual CNI configuration:

sudo rm -rf /etc/cni/net.d
sudo rm -rf /var/lib/cni

Restart containerd:

sudo systemctl restart containerd

Then rerun dry-run.

Validation Checklist

 containerd running

 swap disabled

 no previous cluster state

 kubeadm dry-run successful

If all checks pass, proceed to:

06-control-plane-init.md
