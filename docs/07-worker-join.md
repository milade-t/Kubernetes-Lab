07 — Install CNI (Flannel)

Perform on the control plane node.

1. Apply Flannel Manifest
kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml
2. Verify Flannel Deployment
kubectl get pods -n kube-flannel

Wait until all pods show:

STATUS = Running
3. Verify Node Status
kubectl get nodes

Expected:

STATUS = Ready

If still NotReady, wait 1–2 minutes and check again.

4. Verify CoreDNS
kubectl get pods -n kube-system

CoreDNS should now show:

Running
Validation Checklist

 Flannel pods running

 Node status = Ready

 CoreDNS running

Next step:

08-worker-join.md
