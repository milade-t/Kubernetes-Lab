04 — Install Kubernetes Components

Perform on all nodes.

1. Add Kubernetes Repository

Add GPG key:

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.34/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

Add repository:

echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.34/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

Update package index:

sudo apt update
2. Install kubelet, kubeadm, kubectl
sudo apt install -y kubelet kubeadm kubectl

Prevent automatic upgrades:

sudo apt-mark hold kubelet kubeadm kubectl

Enable kubelet:

sudo systemctl enable kubelet
3. Verify Installation

Check versions:

kubelet --version
kubeadm version
kubectl version --client

All nodes should report the same Kubernetes minor version.

Validation Checklist

On each node confirm:

 Kubernetes repository added

 kubelet installed

 kubeadm installed

 kubectl installed

 kubelet enabled

 packages held

If all checks pass:

On control plane → proceed to 05-preflight-validation.md

On worker → wait until control plane is initialized

Next we build:

05-preflight-validation.md
