### Task 1: Deploy the Application
First, create a Deployment that you will expose with Services. Create `app-deployment.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
  labels:
    app: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
      - name: nginx
        image: nginx:1.25
        ports:
        - containerPort: 80
```

```bash
kubectl apply -f app-deployment.yaml
kubectl get pods -o wide
```

Note the individual Pod IPs. These will change if pods restart — that is the problem Services fix.

<img width="1257" height="168" alt="image" src="https://github.com/user-attachments/assets/6bf683f5-822a-4277-883f-3c30e8d82756" />


**Verify:** Are all 3 pods running? Note down their IP addresses.

```
  IP
  10.244.0.22
  10.244.0.24
  10.244.0.23
```
------

### Task 2: ClusterIP Service (Internal Access)
ClusterIP is the default Service type. It gives your Pods a stable internal IP that is only reachable from within the cluster.

Create `clusterip-service.yaml`:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-app-clusterip
spec:
  type: ClusterIP
  selector:
    app: web-app
  ports:
  - port: 80
    targetPort: 80
```

Key fields:
- `selector.app: web-app` — this Service routes traffic to all Pods with the label `app: web-app`
- `port: 80` — the port the Service listens on
- `targetPort: 80` — the port on the Pod to forward traffic to

```bash
kubectl apply -f clusterip-service.yaml
kubectl get services
```

You should see `web-app-clusterip` with a CLUSTER-IP address. This IP is stable — it will not change even if Pods restart.

Now test it from inside the cluster:
```bash
# Run a temporary pod to test connectivity
kubectl run test-client --image=busybox:latest --rm -it --restart=Never -- sh

# Inside the test pod, run:
wget -qO- http://web-app-clusterip
exit
```
You should see the Nginx welcome page. The Service load-balanced your request to one of the 3 Pods.

<img width="1451" height="597" alt="image" src="https://github.com/user-attachments/assets/d97adb14-44c2-41d1-867e-928178d205d1" />

**Verify:** Does the Service respond? Try running the wget command multiple times — the Service distributes traffic across all healthy Pods.
* yes , the service responded
-------

### Task 3: Discover Services with DNS
Kubernetes has a built-in DNS server. Every Service gets a DNS entry automatically:

```
<service-name>.<namespace>.svc.cluster.local
```

Test this:
```bash
kubectl run dns-test --image=busybox:latest --rm -it --restart=Never -- sh

# Inside the pod:
# Short name (works within the same namespace)
wget -qO- http://web-app-clusterip

# Full DNS name
wget -qO- http://web-app-clusterip.default.svc.cluster.local

# Look up the DNS entry
nslookup web-app-clusterip
exit
```
<img width="1451" height="998" alt="image" src="https://github.com/user-attachments/assets/c43f68bf-aab7-4abc-8b49-b49370d0e04d" />
<img width="817" height="302" alt="image" src="https://github.com/user-attachments/assets/af4075dd-1378-43f6-889f-229573f0feb4" />

Both the short name and the full DNS name resolve to the same ClusterIP. In practice, you use the short name when communicating within the same namespace and the full name when reaching across namespaces.

**Verify:** What IP does `nslookup` return? Does it match the CLUSTER-IP from `kubectl get services`?
* nslookup returns the ClusterIP of the service . yes it matches with `kubectl get services`
  
<img width="677" height="100" alt="image" src="https://github.com/user-attachments/assets/dcf7cbb0-f48e-402c-bdcb-908b2681f93c" />

------

### Task 4: NodePort Service (External Access via Node)
A NodePort Service exposes your application on a port on every node in the cluster. This lets you access the Service from outside the cluster.

Create `nodeport-service.yaml`:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-app-nodeport
spec:
  type: NodePort
  selector:
    app: web-app
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30080
```

- `nodePort: 30080` — the port opened on every node (must be in range 30000-32767)
- Traffic flow: `<NodeIP>:30080` -> Service -> Pod:80

```bash
kubectl apply -f nodeport-service.yaml
kubectl get services
```
<img width="826" height="142" alt="image" src="https://github.com/user-attachments/assets/1127ffb4-df54-4f07-8cee-4323041eef6d" />


Access the service:
```bash
# If using Minikube
minikube service web-app-nodeport --url

# If using Kind, get the node IP first
kubectl get nodes -o wide
# Then curl <node-internal-ip>:30080

# If using Docker Desktop
curl http://localhost:30080
```
<img width="1578" height="573" alt="image" src="https://github.com/user-attachments/assets/35fb8424-c3d8-4ef3-89f3-34fdd436531c" />

**Verify:** Can you see the Nginx welcome page from your browser or terminal using the NodePort?
* yes, nginx html page is diplayed in the terminal
------------
### Task 5: LoadBalancer Service (Cloud External Access)
In a cloud environment (AWS, GCP, Azure), a LoadBalancer Service provisions a real external load balancer that routes traffic to your nodes.

Create `loadbalancer-service.yaml`:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-app-loadbalancer
spec:
  type: LoadBalancer
  selector:
    app: web-app
  ports:
  - port: 80
    targetPort: 80
```

```bash
kubectl apply -f loadbalancer-service.yaml
kubectl get services
```

<img width="863" height="182" alt="image" src="https://github.com/user-attachments/assets/4012d052-ded5-4064-bf43-52488483fb44" />


On a local cluster (Minikube, Kind, Docker Desktop), the EXTERNAL-IP will show `<pending>` because there is no cloud provider to create a real load balancer. This is expected.

If you are using Minikube:
```bash
# Minikube can simulate a LoadBalancer
minikube tunnel
# In another terminal, check again:
kubectl get services
```

In a real cloud cluster, the EXTERNAL-IP would be a public IP address or hostname provisioned by the cloud provider.

**Verify:** What does the EXTERNAL-IP column show? Why is it `<pending>` on a local cluster?
* we need to install MetalLB into the Kind cluster and configure it with the IP address range that matches with Docker network.
  or it can also be solved by doing a port forward : kubectl port-forward svc/web-app-loadbalancer 8080:80

------
### Task 6: Understand the Service Types Side by Side
Check all three services:

```bash
kubectl get services -o wide
```
<img width="931" height="111" alt="image" src="https://github.com/user-attachments/assets/c995216c-ada3-48bd-851b-024d065a0154" />

Compare them:

| Type | Accessible From | Use Case |
|------|----------------|----------|
| ClusterIP | Inside the cluster only | Internal communication between services |
| NodePort | Outside via `<NodeIP>:<NodePort>` | Development, testing, direct node access |
| LoadBalancer | Outside via cloud load balancer | Production traffic in cloud environments |

Each type builds on the previous one:
- LoadBalancer creates a NodePort, which creates a ClusterIP
- So a LoadBalancer service also has a ClusterIP and a NodePort

Verify this:
```bash
kubectl describe service web-app-loadbalancer
```
<img width="617" height="367" alt="image" src="https://github.com/user-attachments/assets/5a36a4e7-dbb6-41b2-880d-1213990fd216" />

You should see all three: a ClusterIP, a NodePort, and the LoadBalancer configuration.

**Verify:** Does the LoadBalancer service also have a ClusterIP and NodePort assigned?
* yes
---------

### Task 7: Clean Up
```bash
kubectl delete -f app-deployment.yaml
kubectl delete -f clusterip-service.yaml
kubectl delete -f nodeport-service.yaml
kubectl delete -f loadbalancer-service.yaml

kubectl get pods
kubectl get services
```
<img width="878" height="278" alt="image" src="https://github.com/user-attachments/assets/6bf5dd0f-0190-4a95-8307-50d7d6500a0e" />

Only the built-in `kubernetes` service in the default namespace should remain.

**Verify:** Is everything cleaned up?
* yes
