### Task 1: Create Your First Pod (Nginx)
Create a file called `nginx-pod.yaml`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80
```

Apply it:
```bash
kubectl apply -f nginx-pod.yaml
```

Verify:
```bash
kubectl get pods
kubectl get pods -o wide
```

<img width="1122" height="740" alt="image" src="https://github.com/user-attachments/assets/b1b6a178-7f51-4fc4-ac6c-571a2b8f67cf" />


Wait until the STATUS shows `Running`. Then explore:

# Detailed info about the pod
```
kubectl describe pod nginx-pod
```
<img width="1601" height="931" alt="image" src="https://github.com/user-attachments/assets/d216aab6-4cb8-4b08-9543-0b624f40e5a2" />

# Read the logs
```
kubectl logs nginx-pod
```
<img width="872" height="333" alt="image" src="https://github.com/user-attachments/assets/3dde9e0d-1667-4a6d-a6f1-730ffbd9af5c" />


# Get a shell inside the container
```
kubectl exec -it nginx-pod -- /bin/bash
```
# Inside the container, run:
```
curl localhost:80
exit
```
<img width="821" height="560" alt="image" src="https://github.com/user-attachments/assets/318bb7c5-2335-42af-9bbb-5179eed92db7" />

**Verify:** Can you see the Nginx welcome page when you curl from inside the pod?
* yes , we can see the Nginx html page

-------
### Task 2: Create a Custom Pod (BusyBox)
Write a new manifest `busybox-pod.yaml` from scratch (do not copy-paste the nginx one):

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: busybox-pod
  labels:
    app: busybox
    environment: dev
spec:
  containers:
  - name: busybox
    image: busybox:latest
    command: ["sh", "-c", "echo Hello from BusyBox && sleep 3600"]
```

Apply and verify:
```bash
kubectl apply -f busybox-pod.yaml
kubectl get pods
kubectl logs busybox-pod
```

Notice the `command` field — BusyBox does not run a long-lived server like Nginx. Without a command that keeps it running, the container would exit immediately and the pod would go into `CrashLoopBackOff`.

<img width="775" height="571" alt="image" src="https://github.com/user-attachments/assets/11629a90-a15f-4c52-add0-f9f6a9b8c823" />

**Verify:** Can you see "Hello from BusyBox" in the logs?
* yes , we can see the command in logs

---------

### Task 3: Imperative vs Declarative
You have been using the declarative approach (writing YAML, then `kubectl apply`). Kubernetes also supports imperative commands:

```bash
# Create a pod without a YAML file
kubectl run redis-pod --image=redis:latest

# Check it
kubectl get pods
```
<img width="851" height="125" alt="image" src="https://github.com/user-attachments/assets/52ae4a13-d812-4013-9294-4addf3f32c0c" />


Now extract the YAML that Kubernetes generated:
```bash
kubectl get pod redis-pod -o yaml
```
<img width="797" height="997" alt="image" src="https://github.com/user-attachments/assets/42e5ec43-5c6e-4516-8587-5c86a049b282" />
<img width="1021" height="997" alt="image" src="https://github.com/user-attachments/assets/5a45b545-a40b-4030-9618-7e12abbd6c59" />
<img width="588" height="200" alt="image" src="https://github.com/user-attachments/assets/8e1abe07-be5b-4ce2-9686-b7d7c92627e2" />

Compare this output with your hand-written manifests. Notice how much extra metadata Kubernetes adds automatically (status, timestamps, uid, resource version).

You can also use dry-run to generate YAML without creating anything:
```bash
kubectl run test-pod --image=nginx --dry-run=client -o yaml
```
This is a powerful trick — use it to quickly scaffold a manifest, then customize it.

<img width="1137" height="306" alt="image" src="https://github.com/user-attachments/assets/5bf9a713-e781-4992-8264-1e209730d7a4" />

**Verify:** Save the dry-run output to a file and compare its structure with your nginx-pod.yaml. What fields are the same? What is different?

* Extra fields other than our nginx-pod.yml:
```  
metadata:

  labels:  
    run: test-pod

spec:


    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}

```
---------

### Task 4: Validate Before Applying
Before applying a manifest, you can validate it:

```bash
# Check if the YAML is valid without actually creating the resource
kubectl apply -f nginx-pod.yaml --dry-run=client

# Validate against the cluster's API (server-side validation)
kubectl apply -f nginx-pod.yaml --dry-run=server
```

Now intentionally break your YAML (remove the `image` field or add an invalid field) and run dry-run again. See what error you get.

**Verify:** What error does Kubernetes give when the image field is missing?
* The Pod "nginx-pod" is invalid: spec.containers[0].image: Required value

<img width="842" height="442" alt="image" src="https://github.com/user-attachments/assets/e3c8ecf3-22c5-44a6-8fb5-5def24e66651" />

-------

### Task 5: Pod Labels and Filtering
Labels are how Kubernetes organizes and selects resources. You added labels in your manifests — now use them:

```bash
# List all pods with their labels
kubectl get pods --show-labels

# Filter pods by label
kubectl get pods -l app=nginx
kubectl get pods -l environment=dev

# Add a label to an existing pod
kubectl label pod nginx-pod environment=production

# Verify
kubectl get pods --show-labels

# Remove a label
kubectl label pod nginx-pod environment-
```
<img width="920" height="401" alt="image" src="https://github.com/user-attachments/assets/4c072429-332b-4f47-8f23-2b498828a383" />

Write a manifest for a third pod with at least 3 labels (app, environment, team). Apply it and practice filtering.

<img width="1022" height="277" alt="image" src="https://github.com/user-attachments/assets/776aa037-6c32-4b62-8a0e-0b0cdb21f099" />

-----
### Task 6: Clean Up
Delete all the pods you created:

```bash
# Delete by name
kubectl delete pod nginx-pod
kubectl delete pod busybox-pod
kubectl delete pod redis-pod

# Or delete using the manifest file
kubectl delete -f nginx-pod.yaml

# Verify everything is gone
kubectl get pods
```

<img width="851" height="320" alt="image" src="https://github.com/user-attachments/assets/394a812f-7c05-4d04-a84c-924fd8c1688c" />


Notice that when you delete a standalone Pod, it is gone forever. There is no controller to recreate it. This is why in production you use Deployments (coming on Day 52) instead of bare Pods.

------



