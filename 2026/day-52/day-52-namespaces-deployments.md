### Task 1: Explore Default Namespaces
Kubernetes comes with built-in namespaces. List them:

```bash
kubectl get namespaces
```

You should see at least:
- `default` — where your resources go if you do not specify a namespace
- `kube-system` — Kubernetes internal components (API server, scheduler, etc.)
- `kube-public` — publicly readable resources
- `kube-node-lease` — node heartbeat tracking

Check what is running inside `kube-system`:
```bash
kubectl get pods -n kube-system
```

<img width="823" height="312" alt="image" src="https://github.com/user-attachments/assets/5d51e883-b3b9-4421-87f2-d61a5b2af55f" />

These are the control plane components keeping your cluster alive. Do not touch them.

**Verify:** How many pods are running in `kube-system`?
* 8 pods
-------

### Task 2: Create and Use Custom Namespaces
Create two namespaces — one for a development environment and one for staging:

```bash
kubectl create namespace dev
kubectl create namespace staging
```

Verify they exist:
```bash
kubectl get namespaces
```
<img width="703" height="247" alt="image" src="https://github.com/user-attachments/assets/b00d36a7-225b-4d01-93bd-a6a4d104c1b1" />

You can also create a namespace from a manifest:
```yaml
# namespace.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: production
```

```bash
kubectl apply -f namespace.yaml
```

Now run a pod in a specific namespace:
```bash
kubectl run nginx-dev --image=nginx:latest -n dev
kubectl run nginx-staging --image=nginx:latest -n staging
```

List pods across all namespaces:
```bash
kubectl get pods -A
```

Notice that `kubectl get pods` without `-n` only shows the `default` namespace. You must specify `-n <namespace>` or use `-A` to see everything.

**Verify:** Does `kubectl get pods` show these pods? What about `kubectl get pods -A`?

<img width="1017" height="618" alt="image" src="https://github.com/user-attachments/assets/0aab6e50-94b7-451e-9d87-f882239457b4" />

------

### Task 3: Create Your First Deployment
A Deployment tells Kubernetes: "I want X replicas of this Pod running at all times." If a Pod crashes, the Deployment controller recreates it automatically.

Create a file `nginx-deployment.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: dev
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.24
        ports:
        - containerPort: 80
```

Key differences from a standalone Pod:
- `kind: Deployment` instead of `kind: Pod`
- `apiVersion: apps/v1` instead of `v1`
- `replicas: 3` tells Kubernetes to maintain 3 identical pods
- `selector.matchLabels` connects the Deployment to its Pods
- `template` is the Pod template — the Deployment creates Pods using this blueprint

Apply it:
```bash
kubectl apply -f nginx-deployment.yaml
```

Check the result:
```bash
kubectl get deployments -n dev
kubectl get pods -n dev
```

You should see 3 pods with names like `nginx-deployment-xxxxx-yyyyy`.

<img width="945" height="233" alt="image" src="https://github.com/user-attachments/assets/9a876e75-6cc6-4618-9dfc-bc5a851c5d3d" />

**Verify:** What do the READY, UP-TO-DATE, and AVAILABLE columns mean in the deployment output?

- READY: Shows how many replicas (pods) are currently active and available to users out of the total number you requested (e.g., 3/3).

         ex: READY (2/3) Two pods are running, but you want three.
       
- UP-TO-DATE: Shows how many replicas have been updated to match your most recent deployment configuration.

         ex: UP-TO-DATE (1): Only one pod is running the brand-new version of your code.
            
- AVAILABLE: Shows how many replicas are running and have successfully passed their readiness probes for the required minimum time.

         ex: AVAILABLE (2): Two pods are stable enough to handle user traffic right now.

--------

### Task 5: Scale the Deployment
Change the number of replicas:

```bash
# Scale up to 5
kubectl scale deployment nginx-deployment --replicas=5 -n dev
kubectl get pods -n dev

# Scale down to 2
kubectl scale deployment nginx-deployment --replicas=2 -n dev
kubectl get pods -n dev
```
Watch how Kubernetes creates or terminates pods to match the desired count.

<img width="1163" height="320" alt="image" src="https://github.com/user-attachments/assets/18176d5d-63cb-4476-a0a0-d4d7d4dd64fc" />

You can also scale by editing the manifest — change `replicas: 4` in your YAML file and run `kubectl apply -f nginx-deployment.yaml` again.

<img width="951" height="746" alt="image" src="https://github.com/user-attachments/assets/b9096ff2-d1f0-43ea-bb96-0bc3c89c0b95" />

**Verify:** When you scaled down from 5 to 2, what happened to the extra pods?
* after scaling-down, the pods were terminated .
--------

### Task 6: Rolling Update
Update the Nginx image version to trigger a rolling update:

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.25 -n dev
```

Watch the rollout in real time:
```bash
kubectl rollout status deployment/nginx-deployment -n dev
```
Kubernetes replaces pods one by one — old pods are terminated only after new ones are healthy. This means zero downtime.

Check the rollout history:
```bash
kubectl rollout history deployment/nginx-deployment -n dev
```

Now roll back to the previous version:
```bash
kubectl rollout undo deployment/nginx-deployment -n dev
kubectl rollout status deployment/nginx-deployment -n dev
```

Verify the image is back to the previous version:
```bash
kubectl describe deployment nginx-deployment -n dev | grep Image
```
<img width="1898" height="337" alt="image" src="https://github.com/user-attachments/assets/24d0f6a5-790d-4943-a8a3-e8e545b36d8f" />

**Verify:** What image version is running after the rollback?
```
    Image:         nginx:1.24
```
------

### Task 7: Clean Up
```bash
kubectl delete deployment nginx-deployment -n dev
kubectl delete pod nginx-dev -n dev
kubectl delete pod nginx-staging -n staging
kubectl delete namespace dev staging production
```
Deleting a namespace removes everything inside it. Be very careful with this in production.

<img width="1065" height="175" alt="image" src="https://github.com/user-attachments/assets/cdf719a4-aceb-4f43-9867-f14d61b144c0" />

```bash
kubectl get namespaces
kubectl get pods -A
```
<img width="1027" height="336" alt="image" src="https://github.com/user-attachments/assets/421da924-9f86-4169-9811-93185f3ec6e2" />

**Verify:** Are all your resources gone?
* yes 
--------

