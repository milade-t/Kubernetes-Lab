# 01 – System Requirements

This guide assumes a **clean Linux machine** with no Kubernetes components installed.

---

## 1. Operating System

Install one of the following:

- Ubuntu 22.04 LTS (recommended)
- Debian 12

Verify OS:

```bash
cat /etc/os-release
```

---

## 2. Hardware Requirements (Per Node)

### Minimum

- 2 CPU
- 4GB RAM
- 30GB Disk

### Recommended

- 2–4 CPU
- 8GB RAM
- 40GB Disk

Check CPU:

```bash
nproc
```

Check Memory:

```bash
free -h
```

Check Disk:

```bash
df -h
```

Ensure at least 20GB free before starting.

---

## 3. Unique Hostname

Each node must have a unique hostname.

Check:

```bash
hostnamectl
```

Set if needed:

```bash
sudo hostnamectl set-hostname control-plane
```

---

## 4. Network Connectivity

Nodes must reach each other via IP.

Test:

```bash
ping <other-node-ip>
```

Control plane must allow port 6443.

---

## 5. Clean System Validation

This must be a fresh system.

Check for existing Kubernetes directories:

```bash
ls /etc/kubernetes
```

If directory exists and this is not a reinstall, stop and clean the system.

---

## 6. Swap Must Be Disabled

Check:

```bash
swapon --show
```

If swap is enabled, it will be disabled during Linux preparation.

---

## Pre-Deployment Checklist

- Minimum hardware satisfied
- Unique hostname configured
- Network connectivity verified
- No previous Kubernetes installation

If all checks pass, proceed to:

👉 `02-linux-preparation.md`
