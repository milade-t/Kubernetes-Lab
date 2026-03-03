# 05 – Preflight Validation (Control Plane)

Perform these checks on the **control plane node** before initializing the cluster.

---

## 1. Confirm containerd Is Running

```bash
sudo systemctl status containerd
```

Expected:

```
active (running)
```

---

## 2. Confirm kubelet Is Enabled

```bash
sudo systemctl status kubelet
```

Note:

- kubelet may show errors before cluster initialization.
- This is normal.

---

## 3. Confirm Swap Is Disabled

```bash
swapon --show
```

No output should appear.

---

## 4. Run kubeadm Preflight Dry-Run

```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --dry-run
```

Expected:

- No fatal errors
- Preflight checks pass

If errors occur, common causes include:

- Swap enabled
- Ports already in use
- Old cluster state
- Container runtime not detected

---

## 5. If Reinitializing (Cleanup)

If this node was previously used for Kubernetes:

```bash
sudo kubeadm reset -f
```

Remove residual CNI configuration:

```bash
sudo rm -rf /etc/cni/net.d
sudo rm -rf /var/lib/cni
```

Restart containerd:

```bash
sudo systemctl restart containerd
```

Then rerun the dry-run command.

---

## Validation Checklist

- containerd running
- swap disabled
- no previous cluster state
- kubeadm dry-run successful

If all checks pass, proceed to:

👉 `06-control-plane-init.md`
