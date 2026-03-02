06 — Initialize Control Plane

Perform on the control plane node only.

1. Initialize Cluster
sudo kubeadm init --pod-network-cidr=10.244.0.0/16

Wait until initialization completes.

At the end, kubeadm will print:

Join command (save this)

Instructions to configure kubectl

2. Configure kubectl Access

Run as your normal user:

mkdir -p $HOME/.kube
sudo cp /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

Test access:

kubectl get nodes

Expected:

STATUS = NotReady

This is normal until CNI is installed.

3. Confirm Control Plane Pods
kubectl get pods -n kube-system

You should see:

kube-apiserver

kube-controller-manager

kube-scheduler

etcd

kube-proxy

CoreDNS will show Pending until CNI is installed.

4. Save Worker Join Command

If you did not copy the join command, regenerate it:

kubeadm token create --print-join-command

Save this for worker node setup.

Validation Checklist

 kubeadm init completed successfully

 kubectl configured

 control plane pods running

 join command saved

Next step:

07-install-cni.md
