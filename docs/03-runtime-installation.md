03 — Install and Configure Container Runtime (containerd)

Perform these steps on all nodes.

1. Install containerd
sudo apt update
sudo apt install -y containerd

Verify installation:

containerd --version
2. Generate Default Configuration

Create configuration directory:

sudo mkdir -p /etc/containerd

Generate default config:

sudo containerd config default | sudo tee /etc/containerd/config.toml
3. Enable Systemd Cgroup Driver

Edit configuration:

sudo nano /etc/containerd/config.toml

Find:

SystemdCgroup = false

Change to:

SystemdCgroup = true

Save and exit.

4. Restart and Enable containerd
sudo systemctl restart containerd
sudo systemctl enable containerd

Verify service is active:

sudo systemctl status containerd

Expected state:

active (running)
5. Validate Cgroup Setting
containerd config dump | grep SystemdCgroup

Expected:

SystemdCgroup = true
Validation Checklist

On each node confirm:

 containerd installed

 config.toml generated

 SystemdCgroup = true

 containerd running

If all checks pass, proceed to:

04-kubernetes-installation.md
