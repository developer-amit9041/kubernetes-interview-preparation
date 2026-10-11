# Kubernetes Interview Answers

Detailed Kubernetes interview answers with English definitions, Hindi definitions, Hinglish explanations, practical examples, commands, diagrams, comparison tables, and interview-ready summaries.

---

## Q1. What is Kubernetes?

### 1. English Definition

Kubernetes (also called K8s) is an open-source container orchestration platform that automates the deployment, scaling, networking, and management of containerized applications.

### 2. Hindi Definition

Kubernetes ek open-source platform hai jo containers mein chalne wali applications ko deploy, scale aur manage karne ke kaam aata hai. Ye application ke desired state ko maintain karne aur containerized workloads ko cluster mein manage karne mein help karta hai.

### 3. Hinglish Explanation

Maan lo aapne MERN stack application banayi hai:
- React frontend
- Node.js backend
- MongoDB database

Docker se aap in applications ki images bana kar containers run kar sakte ho. Lekin jaise-jaise application grow hoti hai, aapko multiple replicas, failures, networking, updates aur different machines par workloads manage karne padte hain.

Kubernetes in tasks ko automate karne ke liye orchestration provide karta hai. Aap YAML file mein desired configuration define karte ho, aur Kubernetes controllers actual state ko us desired state ke kareeb rakhne ke liye kaam karte hain.

### 4. Practical Example

Example Deployment that requests three NGINX replicas:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
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
          image: nginx:stable
          ports:
            - containerPort: 80
```

Apply and inspect it:

```bash
kubectl apply -f deployment.yaml
kubectl get deployments
kubectl get pods
kubectl get pods -o wide
```

- `replicas: 3` expresses the desired number of Pods.
- The Deployment controller manages a ReplicaSet to maintain that replica count.
- If a Pod disappears, Kubernetes can create a replacement.
- A Deployment does not by itself make the application publicly accessible; configure a Service and, if needed, Ingress or a LoadBalancer.

### 5. Simplified Architecture

```text
                 Kubernetes Cluster
                         |
             +-----------+-----------+
             |                       |
        Control Plane            Worker Nodes
        - API Server             - kubelet
        - etcd                   - Container runtime
        - Scheduler              - Application Pods
        - Controllers
```

### 6. Important Commands

```bash
kubectl cluster-info
kubectl get nodes
kubectl get pods
kubectl get deployments
kubectl describe deployment nginx-deployment
kubectl delete -f deployment.yaml
```

### 7. Interview-Ready Answer

"Kubernetes is an open-source container orchestration platform used to automate the deployment, scaling, and management of containerized applications. It provides capabilities such as declarative configuration, service discovery, controlled rollouts, and recovery of failed workloads."

**Easy Hinglish revision:** Docker containers ko build aur run karne mein help karta hai; Kubernetes containerized workloads ko cluster level par orchestrate aur manage karta hai.

---

## Q2. Why do we need Kubernetes?

### 1. English Definition

Kubernetes is needed to automate the deployment, scaling, and management of containerized applications. It helps maintain the desired state, recover from certain workload failures, and handle changing workloads with less manual intervention.

### 2. Hindi Definition

Kubernetes ki zaroorat containerized applications ko automatically deploy aur manage karne, replicas maintain karne, traffic distribute karne aur application updates ko controlled way mein release karne ke liye hoti hai.

### 3. Hinglish Explanation

Maan lo aapki Node.js application ek Docker container mein chal rahi hai. Starting mein ek container enough ho sakta hai. Lekin production mein:
- Container ya Pod fail ho sakta hai.
- Users aur traffic badh sakte hain.
- Multiple application instances chalane pad sakte hain.
- Application ko update karna hota hai.
- Multiple machines par workloads manage karne hote hain.

In sab ko manually manage karna difficult ho sakta hai. Kubernetes desired state declare karne aur controllers ke through us state ko maintain karne mein help karta hai.

### 4. Practical Example

A Deployment can request three backend replicas:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: node-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: node-app
  template:
    metadata:
      labels:
        app: node-app
    spec:
      containers:
        - name: node-container
          image: my-node-app:1.0
          ports:
            - containerPort: 5000
```

```bash
kubectl apply -f deployment.yaml
kubectl get pods
kubectl scale deployment node-app --replicas=5
```

Kubernetes attempts to maintain the requested replica count. For metric-based automatic scaling, configure a Horizontal Pod Autoscaler and provide the required metrics and resource configuration.

### 5. Main Reasons We Need Kubernetes

| Challenge | How Kubernetes helps |
|---|---|
| Pod failure | Controllers can create replacement Pods to restore desired replicas |
| Increased traffic | Scale replicas manually or configure autoscaling |
| Many workloads | Manage them through declarative resources |
| Application updates | Perform controlled Deployment rollouts |
| Workload networking | Services provide stable endpoints for matching Pods |
| Multiple machines | Schedule workloads across cluster nodes |
| Configuration drift | Reconcile actual state toward desired state |

### 6. Interview-Ready Answer

"We need Kubernetes to automate deployment, scaling, and management of containerized applications. It helps maintain desired replica counts, recover from Pod failures, provide service discovery, and manage controlled rollouts. It is especially useful when applications run across multiple machines or require reliable workload orchestration."

**Easy Hinglish revision:** Jab containers aur application instances zyada ho jaate hain, Kubernetes deployment, scaling, networking aur recovery ko manage karne mein help karta hai. Har application ko Kubernetes ki zaroorat nahi hoti; small applications Docker alone ya Compose se bhi chal sakti hain.

---

## Q3. What are the main benefits of Kubernetes?

### 1. English Definition

Kubernetes provides benefits such as self-healing, scalability, service discovery, load distribution, controlled rollouts, rollback, declarative configuration, and resource-aware scheduling.

### 2. Hindi Definition

Kubernetes ke main benefits hain failed Pods ko replace karna, application replicas scale karna, Services ke through traffic route karna, updates manage karna aur cluster resources ka use manage karna.

### 3. Main Benefits

1. **Self-healing:** Controllers can replace failed or missing Pods to restore desired state. This does not guarantee that the application itself or its dependencies are healthy.
2. **Scalability:** Increase or decrease replicas manually, or configure the Horizontal Pod Autoscaler to scale based on supported metrics.
3. **Service discovery:** Kubernetes Services provide stable names and endpoints for accessing matching Pods.
4. **Load distribution:** A Service can route traffic among eligible backend Pods.
5. **Rolling updates:** Deployments can gradually replace old Pods with new versions.
6. **Rollback:** Deployment revisions can be rolled back when a suitable revision is available.
7. **Declarative configuration:** YAML manifests describe the desired state.
8. **Resource-aware scheduling:** The scheduler considers resource requests and scheduling constraints when placing Pods.
9. **Configuration and secret management:** ConfigMaps and Secrets can supply configuration to workloads, with appropriate security practices.

### 4. Practical Commands

```bash
# Apply desired configuration
kubectl apply -f deployment.yaml

# Inspect replicas and Pods
kubectl get deployments
kubectl get pods

# Scale a Deployment
kubectl scale deployment node-app --replicas=5

# Update an image
kubectl set image deployment/node-app node-container=my-node-app:2.0

# Check rollout
kubectl rollout status deployment/node-app

# Undo to a previous Deployment revision, if available
kubectl rollout undo deployment/node-app
```

### 5. Benefit Summary

| Benefit | Simple meaning |
|---|---|
| Self-healing | Restore desired Pods after failures |
| Scaling | Change or automatically adjust replica count |
| Service discovery | Reach workloads using stable Service names |
| Load distribution | Route Service traffic to eligible Pods |
| Rolling updates | Gradually deploy a new version |
| Rollback | Return to an available prior Deployment revision |
| Resource management | Schedule Pods using resources and constraints |
| Declarative configuration | Define desired state in manifests |

### 6. Interview-Ready Answer

"The main benefits of Kubernetes are self-healing, scalability, service discovery, load balancing through Services, rolling updates, rollback, declarative configuration, and resource-aware scheduling. These capabilities help teams deploy and operate containerized applications consistently across a cluster."

**Easy Hinglish revision:** Kubernetes Pods ki desired count maintain karne, scaling, traffic routing, updates, rollback aur cluster resources manage karne mein help karta hai.

---

## Q4. What is the difference between Kubernetes and Docker?

### 1. English Definition

**Docker** is a platform and set of tools commonly used to build container images and run containers. **Kubernetes** is a container orchestration platform used to deploy, scale, and manage containerized workloads across a cluster.

### 2. Hindi Definition

Docker application ko image mein package karne aur container run karne mein help karta hai. Kubernetes cluster mein containerized applications ko deploy, scale aur manage karta hai.

### 3. Main Difference

Docker and Kubernetes solve different problems and are often used together. Docker can build an image; Kubernetes schedules Pods that use compatible container images.

| Feature | Docker | Kubernetes |
|---|---|---|
| Main purpose | Build images and run containers | Orchestrate containerized workloads |
| Common unit | Container | Pod |
| Image building | Commonly builds images from Dockerfiles | Usually consumes images built elsewhere |
| Scheduling | Runs containers on a host | Schedules Pods across cluster nodes |
| Scaling | Run more containers or use additional tooling | Replica management and configurable autoscaling |
| Failure recovery | Restart policies and other tools | Controllers reconcile workload state |
| Networking | Container networking tools | Services and cluster networking |
| Multi-machine orchestration | Not Docker Engine's primary role | Designed for cluster orchestration |

### 4. Docker Example

Assume the image `my-node-app:1.0` already exists:

```bash
docker run -d --name node-app -p 5000:5000 my-node-app:1.0
docker ps
```

This starts one container and maps host port 5000 to container port 5000.

### 5. Kubernetes Example

A Deployment can request multiple Pod replicas:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: node-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: node-app
  template:
    metadata:
      labels:
        app: node-app
    spec:
      containers:
        - name: node-container
          image: my-node-app:1.0
          ports:
            - containerPort: 5000
```

```bash
kubectl apply -f deployment.yaml
kubectl get pods
```

The cluster must be able to access the image. Kubernetes does not require Docker Engine specifically; modern clusters commonly use runtimes such as containerd or CRI-O.

### 6. How They Work Together

```text
Application code
      |
Dockerfile and image build
      |
Container image
      |
Image registry (for example, Docker Hub or Amazon ECR)
      |
Kubernetes Deployment
      |
Pods scheduled on cluster nodes
```

### 7. Interview-Ready Answer

"Docker is used to build container images and run containers, while Kubernetes orchestrates containerized workloads across a cluster. Docker helps package and run an application; Kubernetes manages Pod scheduling, replicas, service discovery, and workload recovery. They complement each other rather than being direct replacements."

**Easy Hinglish revision:** Docker = image/container banana aur run karna. Kubernetes = cluster mein Pods aur workloads ko orchestrate karna.

---

## Q5. What is a container?

### 1. English Definition

A **container** is an isolated runtime environment that runs an application process with its required files, dependencies, and configuration. Containers typically share the host operating system's kernel rather than running a separate guest kernel like a virtual machine.

### 2. Hindi Definition

Container ek lightweight, isolated environment hota hai jisme application apni required files aur dependencies ke saath run hoti hai. Isse application ko different compatible environments mein consistently chalane mein help milti hai.

### 3. Hinglish Explanation

Maan lo aapki Node.js application laptop par chalti hai lekin server par dependency ya runtime version ke difference ki wajah se fail ho jaati hai. Container image mein application code, runtime aur required dependencies package karke environment differences ko reduce kiya ja sakta hai. External configuration, secrets, network access aur persistent data ko phir bhi separately manage karna pad sakta hai.

**Remember:** An image is the template; a container is a running instance created from that image.

### 4. Practical Example

Create `app.js`:

```javascript
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("Hello from my container!");
});

app.listen(5000, () => {
  console.log("Server running on port 5000");
});
```

Create `package.json`:

```json
{
  "name": "my-node-app",
  "version": "1.0.0",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "^5.1.0"
  }
}
```

Create a `Dockerfile`:

```dockerfile
FROM node:22-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 5000
CMD ["npm", "start"]
```

Build and run:

```bash
docker build -t my-node-app .
docker run -d --name my-app -p 5000:5000 my-node-app
```

Open `http://localhost:5000` to see the response, provided the application starts successfully and port 5000 is available.

### 5. Container vs Image vs Virtual Machine

| Feature | Container | Container image | Virtual machine |
|---|---|---|---|
| Purpose | Runs application process(es) | Template used to create containers | Runs a guest OS on virtualized hardware |
| State | Runtime instance; may be writable | Immutable/read-only layers by design | Has its own virtual disks and OS state |
| Kernel | Shares host kernel | Does not run by itself | Guest OS has its own kernel |
| Resource footprint | Usually lightweight | Stored image layers | Usually more resource-intensive |

### 6. Interview-Ready Answer

"A container is a lightweight, isolated runtime environment used to run an application with its required dependencies and configuration. Containers typically share the host OS kernel, making them generally more lightweight than virtual machines. Container images provide the template used to create containers, helping applications run consistently across environments."

**Easy Hinglish revision:** Dockerfile se image banti hai; image se container run hota hai. Container application ko isolated runtime environment deta hai.

---

## Q6. What is the difference between Kubernetes and Docker Compose?

### 1. English Definition

**Docker Compose** is a tool for defining and running multi-container applications using a YAML file, commonly on a single host. **Kubernetes** orchestrates containerized workloads across a cluster and provides declarative workload management.

### 2. Hindi Definition

Docker Compose ek YAML file ke through multiple services ko configure aur ek saath run karne mein help karta hai. Kubernetes cluster mein workloads ko deploy, scale aur manage karta hai.

### 3. Main Differences

| Feature | Docker Compose | Kubernetes |
|---|---|---|
| Typical use | Local development, testing, and simpler deployments | Cluster orchestration |
| Configuration | `compose.yaml` | Kubernetes manifests |
| Workload unit | Service/container | Pod and workload resources |
| Setup | Relatively simple | More cluster components and configuration |
| Scaling | Scale services with Compose commands | Replica controllers and configurable autoscaling |
| Scheduling | Commonly one Docker host | Across eligible cluster nodes |
| Updates | Compose manages services, but is not a full cluster rollout system | Deployments support controlled rollouts and revisions |
| Networking | Compose network and service names | Cluster networking and Kubernetes Services |

Compose is not limited to development, and Kubernetes is not mandatory for every production application. Choose based on operational requirements.

### 4. Docker Compose Example

Example `compose.yaml` for backend and MongoDB:

```yaml
services:
  backend:
    build: ./backend
    ports:
      - "5000:5000"
    depends_on:
      - mongodb

  mongodb:
    image: mongo:8
    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
```

Start and inspect:

```bash
docker compose up -d
docker compose ps
```

The backend can connect to MongoDB using hostname `mongodb` and port `27017` on the Compose network. `depends_on` controls startup ordering; it does not by itself guarantee the database is ready to accept connections.

### 5. Kubernetes Example

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: backend
  template:
    metadata:
      labels:
        app: backend
    spec:
      containers:
        - name: backend
          image: my-backend:1.0
          ports:
            - containerPort: 5000
```

```bash
kubectl apply -f backend-deployment.yaml
kubectl get deployments
kubectl get pods
```

This requests three backend Pod replicas. A Service is generally needed to provide a stable endpoint to other workloads.

### 6. Interview-Ready Answer

"Docker Compose defines and runs multi-container applications, commonly on a single host, using a Compose YAML file. Kubernetes orchestrates containerized workloads across a cluster and provides scheduling, replica management, service discovery, and controlled rollouts. Compose is simpler for many local development setups, while Kubernetes is useful when cluster-level orchestration is required."

**Easy Hinglish revision:** Compose ek machine par multiple services ko simple tarike se run karta hai; Kubernetes cluster mein workloads ko orchestrate karta hai.

---

## Q7. What is Kubernetes architecture?

### 1. English Definition

Kubernetes architecture is the organization of a Kubernetes cluster into a **Control Plane** and **Worker Nodes**. The Control Plane manages cluster state and workload scheduling, while Worker Nodes run application workloads in Pods.

### 2. Hindi Definition

Kubernetes architecture batata hai ki cluster ke components kaise arranged hain aur ek doosre ke saath kaise communicate karte hain. Control Plane cluster ko manage karta hai; Worker Nodes par application Pods run hote hain.

### 3. Architecture Diagram

```text
                   Kubernetes Cluster
                           |
          +----------------+----------------+
          |                                 |
     Control Plane                     Worker Nodes
     - API Server                      - kubelet
     - etcd                            - Container runtime
     - Scheduler                       - Application Pods
     - Controller Manager              - Networking components
```

### 4. Control Plane Components

- **API Server (`kube-apiserver`):** Exposes the Kubernetes API and handles API requests.
- **etcd:** Distributed key-value store holding Kubernetes cluster state.
- **Scheduler (`kube-scheduler`):** Selects a suitable node for Pods that have not yet been assigned to a node.
- **Controller Manager (`kube-controller-manager`):** Runs controllers that reconcile actual state toward desired state.

### 5. Worker Node Components

- **kubelet:** Agent that ensures Pods assigned to the node run according to their specifications and reports status.
- **Container runtime:** Runs containers; examples include containerd and CRI-O.
- **kube-proxy:** In clusters that use it, maintains network rules for Service networking. Some networking implementations provide alternatives.

### 6. How a Deployment Request Works

When you run `kubectl apply -f deployment.yaml`:

1. `kubectl` sends the request to the API Server.
2. The API Server validates and processes the request, including authorization and admission checks.
3. The desired resource state is persisted in etcd.
4. Deployment and ReplicaSet controllers work to create the requested replicas.
5. The Scheduler selects nodes for newly unscheduled Pods.
6. Node kubelets work with the container runtime to start the containers.
7. Controllers continue reconciling actual state with desired state.

### 7. Useful Commands

```bash
kubectl cluster-info
kubectl get nodes
kubectl get pods -o wide
kubectl get pods -n kube-system
kubectl describe node <node-name>
```

Managed Kubernetes services may hide or provider-manage Control Plane components, so they may not all appear as visible Pods in `kube-system`.

### 8. Interview-Ready Answer

"Kubernetes architecture consists of a Control Plane and Worker Nodes. The API Server handles API requests, etcd stores cluster state, the Scheduler assigns Pods to suitable nodes, and controllers reconcile the desired state. Worker Nodes use kubelet and a container runtime to run application Pods. Service networking is implemented by kube-proxy or an alternative networking solution."

**Easy Hinglish revision:** Control Plane decides and coordinates; Worker Nodes run the workloads.

---

## Q8. What is a Kubernetes cluster?

### 1. English Definition

A **Kubernetes cluster** is a group of machines, called nodes, that work together to run and manage containerized applications. A cluster includes the Control Plane and the nodes on which workloads run.

### 2. Hindi Definition

Kubernetes cluster machines ka group hota hai jo milkar containerized applications ko run aur manage karta hai. Ismein cluster management ke liye Control Plane aur workloads run karne ke liye nodes hote hain.

### 3. Hinglish Explanation

Maan lo aap AWS par multiple EC2 instances ko Kubernetes cluster mein use karte ho. Kubernetes workloads ko available nodes par schedule kar sakta hai. Ek node par multiple Pods run ho sakte hain, subject to resources and scheduling rules.

A cluster ka Control Plane dedicated machines par ho sakta hai, ya learning setup mein same machine par roles combined ho sakte hain. Managed services mein provider Control Plane ko manage kar sakta hai.

### 4. Simplified Diagram

```text
                 Kubernetes Cluster
                         |
              +----------+----------+
              |                     |
         Control Plane           Worker Nodes
         Manages state       Run application Pods
                                   |
                              +----+----+
                              |         |
                            Pod 1     Pod 2
```

### 5. Practical Commands

You can practice locally with Minikube:

```bash
minikube start
kubectl get nodes
kubectl cluster-info
```

These commands assume Minikube and kubectl are installed. A local cluster may use one machine for multiple roles.

### 6. Cluster vs Node vs Pod vs Container

| Term | Meaning | Example |
|---|---|---|
| Cluster | Complete Kubernetes system | Control Plane and nodes |
| Node | Physical or virtual machine | EC2 instance |
| Pod | Smallest deployable workload unit | Pod running a Node.js container |
| Container | Isolated application runtime | Node.js process in a container |

### 7. Interview-Ready Answer

"A Kubernetes cluster is a group of nodes that work together to run and manage containerized applications. The Control Plane manages cluster state and schedules workloads, while nodes run application Pods. Kubernetes provides mechanisms for workload scheduling, scaling, and reconciling the desired state."

**Easy Hinglish revision:** Cluster = Kubernetes ka complete system, jisme Control Plane aur nodes milkar applications manage karte hain.

---

## Q9. What is a node?

### 1. English Definition

A **node** is a physical or virtual machine that is part of a Kubernetes cluster. Depending on its role and cluster configuration, it can host Control Plane components, application workloads, or both.

### 2. Hindi Definition

Kubernetes mein Node ek physical ya virtual machine hoti hai jo cluster ka part hoti hai. Worker Nodes par application Pods run hote hain, aur Control Plane nodes cluster management components chala sakte hain.

### 3. Hinglish Explanation

Maan lo aapke Kubernetes cluster mein teen machines hain. Ek Control Plane ke liye aur do Worker Nodes ke liye use ho sakti hain. Scheduler available resources aur scheduling constraints ke according Pods ko suitable Worker Nodes par place karta hai.

Node ek machine hai, Pod workload unit hai, aur container application process ko run karta hai.

### 4. Useful Commands

```bash
# List nodes
kubectl get nodes

# Inspect a node
kubectl describe node <node-name>

# See which node each Pod is assigned to
kubectl get pods -o wide
```

A node with status `Ready` is reporting that it is ready to accept workloads, subject to scheduling constraints.

### 5. Node vs Pod vs Container

| Term | Meaning |
|---|---|
| Node | Machine in the cluster |
| Pod | Kubernetes workload unit scheduled to a node |
| Container | Runtime that executes the application process |

### 6. Interview-Ready Answer

"A node is a physical or virtual machine in a Kubernetes cluster. Worker Nodes run application Pods and include kubelet and a container runtime. The Control Plane manages the cluster and coordinates workload scheduling."

**Easy Hinglish revision:** Node = machine, Pod = workload unit, Container = application runtime.

---

## Q10. What is a master node / control plane?

### 1. English Definition

The **Control Plane** is the part of Kubernetes responsible for managing cluster state, coordinating operations, and scheduling workloads. "Master node" is older terminology often used for a machine running Control Plane components.

### 2. Hindi Definition

Control Plane Kubernetes cluster ka management part hai. Ye API requests handle karta hai, cluster state store karwata hai, Pods ke liye nodes select karwata hai aur desired state maintain karne ke liye controllers run karta hai.

### 3. Main Components

| Component | Responsibility |
|---|---|
| API Server | Kubernetes API ka entry point |
| etcd | Cluster state ka persistent key-value store |
| Scheduler | Unscheduled Pods ke liye suitable node select karta hai |
| Controller Manager | Controllers run karta hai jo desired state reconcile karte hain |

### 4. Example: What happens when a Pod fails?

Suppose a Deployment requests three replicas, but one Pod is lost:

1. The Deployment/ReplicaSet controller observes that actual replicas do not match the desired count.
2. It works to create a replacement Pod.
3. If the replacement Pod is not assigned to a node, the Scheduler selects a suitable node.
4. The node's kubelet and container runtime work to run the Pod's containers.

The Control Plane coordinates this process; it does not mean every application failure can be fixed automatically. Application health, configuration, storage, and dependency failures may need additional handling.

### 5. Useful Commands

```bash
kubectl get nodes
kubectl describe node <node-name>
kubectl get pods -n kube-system
```

In kubeadm or many local clusters, Control Plane components may appear as Pods in `kube-system`. Managed Kubernetes providers may manage these components outside the user's direct view.

### 6. Master Node vs Control Plane

| Master Node | Control Plane |
|---|---|
| Older terminology | Preferred current terminology |
| Usually refers to a machine hosting management components | Refers to cluster management functions and components |
| Often described as one machine | Can be distributed across multiple machines for high availability |

### 7. Interview-Ready Answer

"The Control Plane manages a Kubernetes cluster. Its main components are the API Server, etcd, Scheduler, and Controller Manager. The API Server handles requests, etcd stores cluster state, the Scheduler assigns Pods to suitable nodes, and controllers reconcile actual state with desired state. Worker Nodes run application workloads."

**Easy Hinglish revision:** Control Plane cluster ka manager hai; Worker Nodes application workloads run karte hain.

---

## Quick Revision: Questions 1–10

| Q# | Question | Key point |
|---:|---|---|
| 1 | What is Kubernetes? | Container orchestration platform |
| 2 | Why do we need Kubernetes? | Automates workload deployment and management |
| 3 | Main benefits of Kubernetes? | Self-healing, scaling, Services, rollouts |
| 4 | Kubernetes vs Docker? | Container tools vs cluster orchestration |
| 5 | What is a container? | Isolated application runtime |
| 6 | Kubernetes vs Docker Compose? | Cluster orchestration vs multi-container app tool |
| 7 | Kubernetes architecture? | Control Plane and Worker Nodes |
| 8 | What is a cluster? | Group of nodes managed as one Kubernetes system |
| 9 | What is a node? | Physical or virtual machine in the cluster |
| 10 | Master node / Control Plane? | Cluster management components and functions |
