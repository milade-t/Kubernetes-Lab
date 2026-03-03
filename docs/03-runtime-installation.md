# 03 – Install and Configure Container Runtime (containerd)

Perform these steps on **all nodes**.

---

## 1. Install containerd

```bash
sudo apt update
sudo apt install -y containerd
```

Verify installation:

```bash
containerd --version
```

---

## 2. Generate Default Configuration

Create configuration directory:

```bash
sudo mkdir -p /etc/containerd
```

Generate default config:

```bash
sudo containerd config default | sudo tee /etc/containerd/config.toml
```

---

## 3. Enable Systemd Cgroup Driver

Edit configuration:

```bash
sudo nano /etc/containerd/config.toml
```

Find:

```
SystemdCgroup = false
```

Change to:

```
SystemdCgroup = true
```

Save and exit.

---

## 4. Restart and Enable containerd

```bash
sudo systemctl restart containerd
sudo systemctl enable containerd
```

Verify service is active:

```bash
sudo systemctl status containerd
```

Expected state:

```
active (running)
```

---

## 5. Validate Cgroup Setting

```bash
containerd config dump | grep SystemdCgroup
```

Expected:

```
SystemdCgroup = true
```

---

## Validation Checklist

On each node confirm:

- containerd installed
- `/etc/containerd/config.toml` exists
- `SystemdCgroup = true`
- containerd service running

If all checks pass, proceed to:

👉 `04-kubernetes-installation.md`
