# 04 – Install Kubernetes Components

Perform these steps on **all nodes**.

---

## 1. Add Kubernetes Repository

Create keyring directory:

```bash
sudo mkdir -p /etc/apt/keyrings
```

Add GPG key:

```bash
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.34/deb/Release.key \
| sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```

Add repository:

```bash
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] \
https://pkgs.k8s.io/core:/stable:/v1.34/deb/ /" \
| sudo tee /etc/apt/sources.list.d/kubernetes.list
```

Update package index:

```bash
sudo apt update
```

---

## 2. Install kubelet, kubeadm, kubectl

```bash
sudo apt install -y kubelet kubeadm kubectl
```

Prevent automatic upgrades:

```bash
sudo apt-mark hold kubelet kubeadm kubectl
```

Enable kubelet service:

```bash
sudo systemctl enable kubelet
```

---

## 3. Verify Installation

Check versions:

```bash
kubelet --version
kubeadm version
kubectl version --client
```

All nodes should report the same Kubernetes **minor version** (e.g., v1.34.x).

---

## Validation Checklist

On each node confirm:

- Kubernetes repository added
- kubelet installed
- kubeadm installed
- kubectl installed
- kubelet service enabled
- Packages held with `apt-mark`

If all checks pass:

- On **control plane** → proceed to `05-preflight-validation.md`
- On **worker** → wait until control plane is initialized
