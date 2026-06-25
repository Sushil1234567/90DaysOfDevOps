### Task 1: See the Problem — Data Lost on Pod Deletion
1. Write a Pod manifest that uses an `emptyDir` volume and writes a timestamped message to `/data/message.txt`
2. Apply it, verify the data exists with `kubectl exec`
   
   <img width="912" height="1001" alt="image" src="https://github.com/user-attachments/assets/32c5c206-aab4-4c39-bd05-5284c7c8f5a8" />

4. Delete the Pod, recreate it, check the file again — the old message is gone
   
  <img width="822" height="107" alt="image" src="https://github.com/user-attachments/assets/1d773716-a221-4bef-8b31-bd69d19d6512" />
  <img width="907" height="176" alt="image" src="https://github.com/user-attachments/assets/1796dc24-ee15-42f4-bd75-990a3c0ffe97" />

**Verify:** Is the timestamp the same or different after recreation?
* the timestamp is gone, since the pod was deleted and new timestamps were generated after recreation

--------------
### Task 2: Create a PersistentVolume (Static Provisioning)
1. Write a PV manifest with `capacity: 1Gi`, `accessModes: ReadWriteOnce`, `persistentVolumeReclaimPolicy: Retain`, and `hostPath` pointing to `/tmp/k8s-pv-data`
2. Apply it and check `kubectl get pv` — status should be `Available`

Access modes to know:
- `ReadWriteOnce (RWO)` — read-write by a single node
- `ReadOnlyMany (ROX)` — read-only by many nodes
- `ReadWriteMany (RWX)` — read-write by many nodes

`hostPath` is fine for learning, not for production.

<img width="1162" height="537" alt="image" src="https://github.com/user-attachments/assets/ee90bad3-cdb3-4e28-905a-97b0a1617a86" />

**Verify:** What is the STATUS of the PV?
* Status: Available
-------------------------

### Task 3: Create a PersistentVolumeClaim
1. Write a PVC manifest requesting `500Mi` of storage with `ReadWriteOnce` access
2. Apply it and check both `kubectl get pvc` and `kubectl get pv`
3. Both should show `Bound` — Kubernetes matched them by capacity and access mode
   
   <img width="1287" height="711" alt="image" src="https://github.com/user-attachments/assets/5ad29df7-5b4a-4530-b39c-1ffdf07e1b3a" />

**Verify:** What does the VOLUME column in `kubectl get pvc` show?
* VOLUME:pv-manifest
-------------------------------

### Task 4: Use the PVC in a Pod — Data That Survives
1. Write a Pod manifest that mounts the PVC at `/data` using `persistentVolumeClaim.claimName`
2. Write data to `/data/message.txt`, then delete and recreate the Pod
3. Check the file — it should contain data from both Pods
   
   <img width="983" height="950" alt="image" src="https://github.com/user-attachments/assets/28d8970a-f343-4043-8575-4dfc331053e7" />

**Verify:** Does the file contain data from both the first and second Pod?
* yes, both the container data are persisted .
------------------------

### Task 5: StorageClasses and Dynamic Provisioning
1. Run `kubectl get storageclass` and `kubectl describe storageclass`
2. Note the provisioner, reclaim policy, and volume binding mode
   * PROVISIONER: rancher.io/local-path
   * RECLAIMPOLICY: Delete
   * VOLUMEBINDINGMODE: WaitForFirstConsumer
4. With dynamic provisioning, developers only create PVCs — the StorageClass handles PV creation automatically
   
 <img width="1895" height="306" alt="image" src="https://github.com/user-attachments/assets/cee18bef-b005-4a4a-af57-2cd3b12d94b0" />

**Verify:** What is the default StorageClass in your cluster?
* PROVISIONER: rancher.io/local-path
---------

### Task 6: Dynamic Provisioning
1. Write a PVC manifest that includes `storageClassName: standard` (or your cluster's default)
2. Apply it — a PV should appear automatically in `kubectl get pv`
3. Use this PVC in a Pod, write data, verify it works
   
<img width="1277" height="431" alt="image" src="https://github.com/user-attachments/assets/8493d63b-b0fc-4714-8154-56bac02ac702" />
<img width="1532" height="847" alt="image" src="https://github.com/user-attachments/assets/b88cb4d1-9cc5-4f8d-bc27-b0705e0cbdd2" />

**Verify:** How many PVs exist now? Which was manual, which was dynamic?
* there are 2 pv now, one is manual and one standard , the standard one is dynamic.

-----

### Task 7: Clean Up
1. Delete all pods first
2. Delete PVCs — check `kubectl get pv` to see what happened
3. The dynamic PV is gone (Delete reclaim policy). The manual PV shows `Released` (Retain policy).
4. Delete the remaining PV manually

<img width="1548" height="506" alt="image" src="https://github.com/user-attachments/assets/441aca67-5ddc-4aca-ae7b-898c7705e81a" />

**Verify:** Which PV was auto-deleted and which was retained? Why?
* the one that was dynamically created had standard storage class was auto deleted , and the one having manual storage class was retained .
----------




