# 06 – Initialize Control Plane

Perform these steps on the **control plane node only**.

---

## 1. Initialize the Cluster

```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

Wait for initialization to complete.

At the end, kubeadm will print:

- A **worker join command** (save this)
- Instructions to configure `kubectl`

---

## 2. Configure kubectl Access

Run as your normal (non-root) user:

```bash
mkdir -p $HOME/.kube
sudo cp /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Test cluster access:

```bash
kubectl get nodes
```

Expected:

```
STATUS = NotReady
```

This is normal until a CNI plugin is installed.

---

## 3. Confirm Control Plane Pods

```bash
kubectl get pods -n kube-system
```

You should see:

- kube-apiserver
- kube-controller-manager
- kube-scheduler
- etcd
- kube-proxy

CoreDNS will likely show `Pending` until CNI is installed.

---

## 4. Save Worker Join Command

If you did not copy the join command, regenerate it:

```bash
kubeadm token create --print-join-command
```

Save this command for worker node setup.

---

## Validation Checklist

- kubeadm init completed successfully
- kubectl configured correctly
- control plane pods running
- join command saved

Next step:

👉 `07-install-cni.md`
