# 09 – Post-Install Validation

Perform these checks on the **control plane node**.

---

## 1. Confirm Cluster Health

```bash
kubectl get nodes
```

Expected:

```
STATUS = Ready
```

---

## 2. Confirm System Pods

```bash
kubectl get pods -n kube-system
```

All pods should show:

```
STATUS = Running
```

---

## 3. Confirm Networking (Pod-to-Pod)

Deploy a test pod:

```bash
kubectl run testpod --image=nginx --restart=Never
```

Verify it is running:

```bash
kubectl get pods -o wide
```

Note the **Pod IP**.

---

## 4. Deploy Test Deployment

Create a deployment:

```bash
kubectl create deployment nginx-test --image=nginx
```

Expose it as a NodePort service:

```bash
kubectl expose deployment nginx-test --type=NodePort --port=80
```

Check service details:

```bash
kubectl get svc
```

Note the assigned NodePort (example: `30007`).

Access from browser:

```
http://<node-ip>:<nodeport>
```

---

## 5. Confirm Scheduling Behavior

If running a single-node cluster and the control-plane taint still exists, workloads will not schedule.

Remove taint if needed:

```bash
kubectl taint nodes --all node-role.kubernetes.io/control-plane-
```

Verify pods schedule successfully.

---

## 6. Check Node Conditions

```bash
kubectl describe node <node-name>
```

Confirm:

- MemoryPressure = False
- DiskPressure = False
- Ready = True

---

## 7. Optional: Clean Test Workload

```bash
kubectl delete deployment nginx-test
kubectl delete svc nginx-test
kubectl delete pod testpod
```

---

## Final Validation Checklist

- Nodes Ready
- System pods Running
- Test pod deployed successfully
- Service accessible via NodePort
- No DiskPressure or MemoryPressure

Cluster deployment complete.
