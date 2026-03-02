# 02 – Linux Preparation

Perform these steps on **all nodes** (control plane and worker).

---

## 1. Update System

```bash
sudo apt update
sudo apt upgrade -y
```

Reboot if kernel updates were installed:

```bash
sudo reboot
```

---

## 2. Disable Swap (Required)

Disable immediately:

```bash
sudo swapoff -a
```

Disable permanently:

```bash
sudo sed -i '/ swap / s/^/#/' /etc/fstab
```

Verify:

```bash
swapon --show
```

No output should appear.

---

## 3. Load Required Kernel Modules

Create configuration file:

```bash
sudo tee /etc/modules-load.d/k8s.conf <<EOF
overlay
br_netfilter
EOF
```

Load modules:

```bash
sudo modprobe overlay
sudo modprobe br_netfilter
```

Verify:

```bash
lsmod | grep overlay
lsmod | grep br_netfilter
```

---

## 4. Configure Sysctl Parameters

Create sysctl config:

```bash
sudo tee /etc/sysctl.d/k8s.conf <<EOF
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward = 1
EOF
```

Apply settings:

```bash
sudo sysctl --system
```

Verify:

```bash
sysctl net.ipv4.ip_forward
```

Expected:

```
net.ipv4.ip_forward = 1
```

---

## 5. Install Required Base Packages

```bash
sudo apt install -y apt-transport-https ca-certificates curl gnupg lsb-release
```

---

## Validation Checklist

On each node confirm:

- Swap disabled
- `overlay` module loaded
- `br_netfilter` module loaded
- `ip_forward = 1`
- System fully updated

If all checks pass, proceed to:

👉 `03-runtime-installation.md`
