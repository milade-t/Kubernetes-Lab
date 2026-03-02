08 — Join Worker Node

Perform these steps on the worker node.

1. Ensure Prerequisites Completed

On the worker node confirm:

Linux preparation completed

containerd installed and running

Kubernetes components installed

Verify containerd:

sudo systemctl status containerd
2. Run Join Command

Use the join command generated from the control plane:

sudo kubeadm join <control-plane-ip>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>

If join succeeds, you will see:

This node has joined the cluster
3. Verify From Control Plane

On the control plane:

kubectl get nodes

Expected:

control-plane   Ready
worker          Ready

Worker may take 30–60 seconds to transition to Ready.

4. Confirm Worker Pods
kubectl get pods -A -o wide

You should see:

kube-proxy running on worker

flannel daemonset running on worker

Validation Checklist

 join command executed successfully

 worker appears in kubectl get nodes

 worker status = Ready

 flannel running on worker

Next step:

09-post-install-validation.md
