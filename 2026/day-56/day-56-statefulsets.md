### Task 1: Understand the Problem
1. Create a Deployment with 3 replicas using nginx
2. Check the pod names — they are random (`app-xyz-abc`)
3. Delete a pod and notice the replacement gets a different random name

<img width="1005" height="915" alt="image" src="https://github.com/user-attachments/assets/5a553425-f1c1-492b-9263-0092165216d2" />

This is fine for web servers but not for databases where you need stable identity.

| Feature | Deployment | StatefulSet |
|---|---|---|
| Pod names | Random | Stable, ordered (`app-0`, `app-1`) |
| Startup order | All at once | Ordered: pod-0, then pod-1, then pod-2 |
| Storage | Shared PVC | Each pod gets its own PVC |
| Network identity | No stable hostname | Stable DNS per pod |

Delete the Deployment before moving on.
*  kubectl delete deployment nginx-deployment

**Verify:** Why would random pod names be a problem for a database cluster?
* Random pod names are a major problem for a database cluster because they break identity, network routing, and data consistency.
  Stable names, stable network identities, and dedicated storage make those db systems reliable.

----------------

### Task 2: Create a Headless Service
1. Write a Service manifest with `clusterIP: None` — this is a Headless Service
2. Set the selector to match the labels you will use on your StatefulSet pods
3. Apply it and confirm CLUSTER-IP shows `None`

<img width="790" height="440" alt="image" src="https://github.com/user-attachments/assets/1c042572-9ea8-4d2e-b539-e6ced179a0b5" />

A Headless Service creates individual DNS entries for each pod instead of load-balancing to one IP. StatefulSets require this.

**Verify:** What does the CLUSTER-IP column show?
* None
----------------

### Task 3: Create a StatefulSet
1. Write a StatefulSet manifest with `serviceName` pointing to your Headless Service
2. Set replicas to 3, use the nginx image
3. Add a `volumeClaimTemplates` section requesting 100Mi of ReadWriteOnce storage
4. Apply and watch: `kubectl get pods -l <your-label> -w`

Observe ordered creation — `web-0` first, then `web-1` after `web-0` is Ready, then `web-2`.

Check the PVCs: `kubectl get pvc` — you should see `web-data-web-0`, `web-data-web-1`, `web-data-web-2` (names follow the pattern `<template-name>-<pod-name>`).

<img width="727" height="998" alt="image" src="https://github.com/user-attachments/assets/7e644a0c-4fcb-4881-a4a5-b701921c74cb" />
<img width="1437" height="393" alt="image" src="https://github.com/user-attachments/assets/8b449105-bcb6-4500-baf3-ab9d8019ca6e" />

**Verify:** What are the exact pod names and PVC names?
* Pods:
  NAME               
nginx-statefulset-0   
nginx-statefulset-1   
nginx-statefulset-2

 * PVC:
nginx-storage-nginx-statefulset-0   
nginx-storage-nginx-statefulset-1   
nginx-storage-nginx-statefulset-2

-----------

### Task 4: Stable Network Identity
Each StatefulSet pod gets a DNS name: `<pod-name>.<service-name>.<namespace>.svc.cluster.local`

1. Run a temporary busybox pod and use `nslookup` to resolve `web-0.<your-headless-service>.default.svc.cluster.local`
2. Do the same for `web-1` and `web-2`
3. Confirm the IPs match `kubectl get pods -o wide`
   
<img width="790" height="598" alt="image" src="https://github.com/user-attachments/assets/ca5162ac-5747-4d94-9bb5-e1fdc22969c0" />
<img width="1232" height="573" alt="image" src="https://github.com/user-attachments/assets/c75cfe9e-a7e5-405b-9ebf-64ca77232a74" />

**Verify:** Does the nslookup IP match the pod IP?
* No
----------

### Task 5: Stable Storage — Data Survives Pod Deletion
1. Write unique data to each pod: `kubectl exec web-0 -- sh -c "echo 'Data from web-0' > /usr/share/nginx/html/index.html"`
2. Delete `web-0`: `kubectl delete pod web-0`
3. Wait for it to come back, then check the data — it should still be "Data from web-0"

The new pod reconnected to the same PVC.

<img width="1579" height="457" alt="image" src="https://github.com/user-attachments/assets/7d2ed954-9c4f-482a-8229-e2ab3e138b15" />

**Verify:** Is the data identical after pod recreation?
* yes

--------------------

### Task 6: Ordered Scaling
1. Scale up to 5: `kubectl scale statefulset web --replicas=5` — pods create in order (web-3, then web-4)
2. Scale down to 3 — pods terminate in reverse order (web-4, then web-3)
3. Check `kubectl get pvc` — all five PVCs still exist. Kubernetes keeps them on scale-down so data is preserved if you scale back up.
   
<img width="1432" height="457" alt="image" src="https://github.com/user-attachments/assets/ad82fcda-c678-4bbb-8d03-767838d61f67" />

**Verify:** After scaling down, how many PVCs exist?
* 5 PVCs
-------------------------------------

### Task 7: Clean Up
1. Delete the StatefulSet and the Headless Service
2. Check `kubectl get pvc` — PVCs are still there (safety feature)
3. Delete PVCs manually
<img width="998" height="197" alt="image" src="https://github.com/user-attachments/assets/61c4e592-64e1-4d2c-b3f5-c8885ed86124" />

**Verify:** Were PVCs auto-deleted with the StatefulSet?
* No
----------------------




