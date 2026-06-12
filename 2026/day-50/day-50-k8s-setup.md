### Task 1: Recall the Kubernetes Story
Before touching a terminal, write down from memory:

1. Why was Kubernetes created? What problem does it solve that Docker alone cannot?
* Kubernetes was created due to the challenge of managing multiple containers in large scale production.
  The most important issue that docker alone cannot solve is auto scaling and auto healing .
3. Who created Kubernetes and what was it inspired by?
* The main inspiration behind the creation of Kubernetes comes down to two things:
  Google’s internal massive scale systems (Borg) and the rise of Docker.
  In 2013, Docker democratised containerisation by making it easy for any developer to package an app on their laptop.
  Google engineers Craig McLuckie, Joe Beda, and Brendan Burns immediately noticed a critical flaw:
  Docker was built for single machines. They realized the tech industry was about to hit a wall trying to scale Docker, hence created Borg aka Kubernetes
4. What does the name "Kubernetes" mean?
* Kubernetes comes from a greek meaning of a person who is a ship captain , hence having a logo of ship steering wheel.

Do not look anything up yet. Write what you remember from the session, then verify against the official docs.

---------

### Task 2: Draw the Kubernetes Architecture
From memory, draw or describe the Kubernetes architecture. Your diagram should include:

**Control Plane (Master Node):**
- API Server — the front door to the cluster, every command goes through it
- etcd — the database that stores all cluster state
- Scheduler — decides which node a new pod should run on
- Controller Manager — watches the cluster and makes sure the desired state matches reality

**Worker Node:**
- kubelet — the agent on each node that talks to the API server and manages pods
- kube-proxy — handles networking rules so pods can communicate
- Container Runtime — the engine that actually runs containers (containerd, CRI-O)

<img width="2673" height="1576" alt="image" src="https://github.com/user-attachments/assets/ebd8e0d7-0db7-4417-8656-358811f181a9" />

After drawing, verify your understanding:
- What happens when you run `kubectl apply -f pod.yaml`? Trace the request through each component.
  1. run kubectl apply -f pod.yaml
  2. the API server receives the request and registers it in the etcd(database)
  3. the scheduler notices the new request and allocate the job to the available worker(worker nodes) and respond back to the API server
  4. the Kubelet notices the Pod assignement and contacts the local container runtime  and commands it to run the container.
  5. the container runtime checks if the container image exists locally. If not, it pulls it down from the container Dockerhub registry
  6. the Kubelet reports the successful status (Running) back to the API Server. The API Server updates the state in etcd.
     When we run kubectl get pods, the API Server reads this final state from etcd and shows the Pod is healthy and operational.
- What happens if the API server goes down?
  * If the Kubernetes API server goes down, your existing applications will keep running normally,
    but we lose the ability to manage, update, or monitor the cluster
- What happens if a worker node goes down?
  * If a worker node goes down, Kubernetes automatically detects the failure and recreates the lost workloads on other healthy nodes

-----------

### Task 3: Install kubectl
`kubectl` is the CLI tool you will use to talk to your Kubernetes cluster.

Install it:
```bash
# macOS
brew install kubectl

# Linux (amd64)
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

# Windows (with chocolatey)
choco install kubernetes-cli
```

Verify:
```bash
kubectl version --client
```

<img width="927" height="292" alt="image" src="https://github.com/user-attachments/assets/fd286eb3-85d0-4d5d-8b88-013e22828a25" />

----

### Task 4: Set Up Your Local Cluster
Choose **one** of the following. Both give you a fully functional Kubernetes cluster on your machine.

**Option A: kind (Kubernetes in Docker)**
```bash
# Install kind
# macOS
brew install kind

# Linux
curl -Lo ./kind https://kind.sigs.k8s.io/dl/latest/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

# Create a cluster
kind create cluster --name devops-cluster

# Verify
kubectl cluster-info
kubectl get nodes
```

**Option B: minikube**
```bash
# Install minikube
# macOS
brew install minikube

# Linux
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Start a cluster
minikube start



```

<img width="1342" height="501" alt="image" src="https://github.com/user-attachments/assets/b0ed2231-7c38-49f8-81b8-c948fd4a847e" />

# Verify

kubectl cluster-info

kubectl get nodes

<img width="940" height="212" alt="image" src="https://github.com/user-attachments/assets/5a9dadac-7d1c-4b9f-8d5e-e5d8bddd6b7c" />

Write down: Which one did you choose and why?
* used KinD for its speed, running multi-node clusters, and lightweight resource usage
----

### Task 5: Explore Your Cluster
Now that your cluster is running, explore it:

```bash
# See cluster info
kubectl cluster-info
```

# List all nodes
```
kubectl get nodes
```
<img width="937" height="193" alt="image" src="https://github.com/user-attachments/assets/459fab6f-a496-4bc6-b78a-746160411a98" />

# Get detailed info about your node
```
kubectl describe node <node-name>
```
<img width="1482" height="983" alt="image" src="https://github.com/user-attachments/assets/c7f625df-c153-4574-b826-a66bfa7b690e" />

# List all namespaces
```
kubectl get namespaces
```
<img width="612" height="141" alt="image" src="https://github.com/user-attachments/assets/26c111f4-2616-4728-939e-c64bbada9426" />

# See ALL pods running in the cluster (across all namespaces)
```
kubectl get pods -A
```

<img width="982" height="298" alt="image" src="https://github.com/user-attachments/assets/85a9fc66-6045-4203-9aa3-afd4ab804510" />


# Look at the pods running in the `kube-system` namespace:

```bash
kubectl get pods -n kube-system
```
You should see pods like `etcd`, `kube-apiserver`, `kube-scheduler`, `kube-controller-manager`, `coredns`, and `kube-proxy`. 
These are the architecture components you drew in Task 2 — running as pods inside the cluster.

<img width="812" height="302" alt="image" src="https://github.com/user-attachments/assets/29f67be8-5804-49a9-beab-60b4b787238b" />

**Verify:** Can you match each running pod in `kube-system` to a component in your architecture diagram?

 *yes

-------


### Task 6: Practice Cluster Lifecycle
Build muscle memory with cluster operations:

```bash
# Delete your cluster
kind delete cluster --name devops-cluster
# (or: minikube delete)

# Recreate it
kind create cluster --name devops-cluster
# (or: minikube start)

# Verify it is back
kubectl get nodes
```

Try these useful commands:
```bash
# Check which cluster kubectl is connected to
kubectl config current-context

# List all available contexts (clusters)
kubectl config get-contexts

# See the full kubeconfig
kubectl config view
```
