09 — Post-Install Validation

Perform on the control plane node.

1. Confirm Cluster Health
kubectl get nodes

Expected:

STATUS = Ready
2. Confirm System Pods
kubectl get pods -n kube-system

All pods should be:

STATUS = Running
3. Confirm Networking (Pod-to-Pod)

Deploy test pod:

kubectl run testpod --image=nginx --restart=Never

Verify pod running:

kubectl get pods -o wide

Note the Pod IP.

4. Deploy Test Deployment
kubectl create deployment nginx-test --image=nginx

Expose as NodePort:

kubectl expose deployment nginx-test --type=NodePort --port=80

Check service:

kubectl get svc

Note the NodePort (example: 30007).

Access from browser:

http://<node-ip>:<nodeport>
5. Confirm Scheduling

If single-node cluster and control-plane taint still exists:

Remove taint:

kubectl taint nodes --all node-role.kubernetes.io/control-plane-

Verify pods schedule successfully.

6. Check Node Conditions
kubectl describe node <node-name>

Confirm:

MemoryPressure = False

DiskPressure = False

Ready = True

7. Optional: Clean Test Workload
kubectl delete deployment nginx-test
kubectl delete svc nginx-test
kubectl delete pod testpod
Final Validation Checklist

 Nodes Ready

 System pods Running

 Test pod deployed successfully

 Service accessible via NodePort

 No DiskPressure or MemoryPressure

Cluster deployment complete.
