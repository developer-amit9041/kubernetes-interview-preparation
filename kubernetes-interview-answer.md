# Kubernetes Interview Answers

Detailed, topic-wise Kubernetes interview answers with English definitions, Hindi definitions, Hinglish explanations, practical examples, diagrams where useful, commands/configuration, summary tables, and interview-ready answers.

> **Study note:** This file is being organized in the same answer format as the Docker interview-answer guide. Use a test cluster for practical commands, and never commit production credentials or real Secret values.

## Table of Contents

- [Q1. What is Kubernetes?](#q1-what-is-kubernetes)
- [Q2. Why do we need Kubernetes?](#q2-why-do-we-need-kubernetes)
- [Q3. What are the main benefits of Kubernetes?](#q3-what-are-the-main-benefits-of-kubernetes)
- [Q4. What is the difference between Kubernetes and Docker?](#q4-what-is-the-difference-between-kubernetes-and-docker)
- [Q5. What is a container?](#q5-what-is-a-container)
- [Q6. What is the difference between Kubernetes and Docker Compose?](#q6-what-is-the-difference-between-kubernetes-and-docker-compose)
- [Q7. What is Kubernetes architecture?](#q7-what-is-kubernetes-architecture)
- [Q8. What is a Kubernetes cluster?](#q8-what-is-a-kubernetes-cluster)
- [Q9. What is a node?](#q9-what-is-a-node)
- [Q10. What is a master node / control plane?](#q10-what-is-a-master-node--control-plane)

---

## Q1. What is Kubernetes?

### 1. English Definition

**Kubernetes (K8s) is an open-source container orchestration platform that automates the deployment, scaling, networking, and management of containerized applications across a cluster of machines.**

It helps keep applications running in the desired state. For example, if a Deployment is configured for three replicas and one Pod fails, Kubernetes works to create a replacement.

> **Interview tip:** Kubernetes does not build container images. You build an image with a tool such as Docker or BuildKit, publish it to a registry, and reference it in a Kubernetes workload. Kubernetes uses a container runtime, commonly containerd, to run containers.

### 2. Hindi Definition

Kubernetes ek open-source container orchestration platform hai jo cluster ki multiple machines par containerized applications ko deploy, scale, network aur manage karne ke kaam ko automate karta hai. Yeh configured desired state ko maintain karne ki koshish karta hai.

### 3. Hinglish Explanation

Maan lo aapki MERN application ka Node.js backend hai aur aap chahte ho ki uske 3 instances run karein. Aap Deployment mein `replicas: 3` define kar dete ho. Kubernetes Pods ko worker nodes par schedule karta hai aur agar koi Pod fail ho jaye, toh controller replacement create karne ki koshish karta hai.

- **Image:** Application ko run karne ka packaged template.
- **Container:** Image se run hone wala process/environment.
- **Pod:** Kubernetes ki smallest deployable unit; ismein ek ya multiple closely related containers ho sakte hain.
- **Deployment:** Desired replica count aur rollout manage karta hai.
- **Service:** Pods ke group ko stable network endpoint deta hai.

### 4. Practical Example / Code

Create `nginx-deployment.yaml`:

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
          image: nginx:1.27
          ports:
            - containerPort: 80
```

Here, `replicas: 3` declares the desired number of Pods. `containerPort: 80` documents the container's listening port; it does not expose the application outside the cluster by itself.

### 5. Architecture Diagram

```text
Developer / kubectl
        |
        v
+---------------------------+
| Kubernetes Control Plane  |
| API Server | Scheduler    |
| Controllers | etcd        |
+---------------------------+
        |
        v
+------------------+   +------------------+
| Worker Node 1    |   | Worker Node 2    |
| Kubelet          |   | Kubelet          |
| Runtime          |   | Runtime          |
| Pod: NGINX       |   | Pod: NGINX       |
+------------------+   +------------------+
                         /
           -- Service --/
```

### 6. Practical Commands

```bash
kubectl apply -f nginx-deployment.yaml
kubectl get deployments
kubectl get pods -o wide
kubectl describe deployment nginx-deployment
kubectl scale deployment nginx-deployment --replicas=5
kubectl get pods
```

Clean up the test resource:

```bash
kubectl delete -f nginx-deployment.yaml
```

### 7. Summary Table

| Term | Meaning |
|---|---|
| Kubernetes | Container orchestration platform |
| Pod | Smallest deployable Kubernetes unit |
| Deployment | Manages stateless application replicas and rollouts |
| Service | Stable endpoint for reaching selected Pods |
| Desired state | The state declared in the workload configuration |

**Interview-ready summary:** Kubernetes automates the deployment, scaling, and management of containerized applications. It runs workloads in Pods across a cluster and uses controllers to reconcile the actual state toward the desired state.

---

## Q2. Why do we need Kubernetes?

### 1. English Definition

Kubernetes is used to manage containerized applications reliably at scale by automating scheduling, recovery, scaling, service discovery, and controlled application updates across a cluster.

### 2. Hindi Definition

Kubernetes ki zaroorat tab hoti hai jab humein multiple containers ko multiple machines par reliably run aur manage karna ho. Yeh deployment, scaling, failed workload recovery aur networking jaise tasks automate karta hai.

### 3. Hinglish Explanation

Maan lo aapki MERN application ke users badh rahe hain. Sirf ek backend container par depend karne se traffic spike ya container failure ke time problem aa sakti hai. Kubernetes mein aap multiple replicas declare kar sakte ho, Service se un tak traffic route kar sakte ho aur resource demand ke according scaling configure kar sakte ho.

Kubernetes useful hai jab:
- Multiple application instances manage karne hon.
- Failed Pods ko replace karna ho.
- Rolling updates aur rollbacks chahiye hon.
- Multiple nodes par workloads schedule karne hon.
- Service discovery aur configuration manage karni ho.
- Resource requests, limits, and autoscaling configure karna ho.

**Important:** Chhote single-container project ke liye Kubernetes zaroori nahi hota. Simple workloads ke liye Docker Compose ya managed application hosting easier ho sakti hai.

### 4. Practical Example / Code

Deployment mein desired replica count set karein:

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
          image: example/backend:1.0
          ports:
            - containerPort: 5000
```

`example/backend:1.0` ko apni registry mein available real image se replace karein.

### 5. Architecture Diagram

```text
             User Requests
                   |
                   v
              Kubernetes
                   |
           +-------+-------+
           |       |       |
           v       v       v
         Pod 1   Pod 2   Pod 3
                  |      /
            --- Service-/
                   |
          Desired replicas maintained
          and failed Pods replaced
```

### 6. Practical Commands

```bash
kubectl apply -f backend-deployment.yaml
kubectl get deployment backend
kubectl get pods -l app=backend
kubectl scale deployment backend --replicas=5
```

### 7. Summary Table

| Need | Kubernetes capability |
|---|---|
| Multiple replicas | Deployment and ReplicaSet |
| Pod failure recovery | Controllers recreate replacement Pods when possible |
| Controlled updates | Rolling updates and rollbacks |
| Internal discovery | Services and cluster DNS |
| Scaling | Manual scaling and autoscalers |
| Multi-machine workloads | Scheduler places Pods on eligible nodes |

**Interview-ready summary:** We use Kubernetes to automate container scheduling, recovery, scaling, networking, and application rollouts. It is most useful when applications need to be managed across a cluster rather than as a few manually operated containers.

---

## Q3. What are the main benefits of Kubernetes?

### 1. English Definition

Kubernetes provides declarative workload management, automated scheduling, self-healing behavior, service discovery, controlled rollouts, resource management, and scaling capabilities for containerized applications.

### 2. Hindi Definition

Kubernetes ke main benefits hain deployment automation, failed Pods ko replace karne ki capability, scaling, service discovery, controlled updates aur cluster resources ka better management.

### 3. Hinglish Explanation

Kubernetes ko aap ek system samjho jahan aap desired state batate ho aur Kubernetes us state ko achieve karne ki koshish karta hai. Aapko har Pod ko manually start karna, traffic ke liye manually har Pod ka IP maintain karna, ya har rollout ko manually orchestrate karna nahi padta.

Main benefits:
- **Self-healing:** Controllers failed/missing Pods ko replace karne ki koshish karte hain.
- **Scaling:** Replica count manually ya autoscaling se badhaya ja sakta hai.
- **Service discovery:** Service aur DNS se workloads ko stable names mil sakte hain.
- **Rollouts and rollbacks:** Application versions ko controlled way mein update kiya ja sakta hai.
- **Resource management:** CPU/memory requests aur limits specify kar sakte hain.
- **Portability:** Kubernetes API aur manifests ko different Kubernetes environments mein adapt kiya ja sakta hai.

Kubernetes high availability guarantee nahi karta by default. Application replicas, node distribution, storage, health checks, networking aur cluster design sahi configure karna bhi zaroori hai.

### 4. Practical Example / Code

Resource requests and limits ka example:

```yaml
resources:
  requests:
    cpu: "100m"
    memory: "128Mi"
  limits:
    cpu: "500m"
    memory: "256Mi"
```

Yeh snippet container ke andar add hota hai. Requests scheduler ko placement ke liye resource requirement batate hain; limits container resource use ko constrain karte hain, with behavior depending on the resource type.

### 5. Architecture Diagram

```text
Desired Configuration (YAML)
             |
             v
       Kubernetes API
             |
             v
    Controllers / Scheduler
             |
     +-------+-------+
     |               |
     v               v
  Schedule Pods   Reconcile state
     |               |
     +-------+-------+
             v
     Application Workloads
```

### 6. Practical Commands

```bash
kubectl get pods -o wide
kubectl rollout status deployment/backend
kubectl scale deployment backend --replicas=4
kubectl describe pod <pod-name>
```

Replace `<pod-name>` with an actual Pod name.

### 7. Summary Table

| Benefit | What it provides |
|---|---|
| Self-healing | Reconciliation and replacement of failed/missing Pods |
| Scaling | Changes in replica count; autoscaling when configured |
| Service discovery | Stable Service names/endpoints |
| Rollouts | Controlled updates to workloads |
| Resource management | Requests, limits, and scheduling based on resources |
| Portability | Reusable declarative manifests with environment-specific adjustments |

**Interview-ready summary:** Kubernetes helps teams operate containerized applications through declarative configuration, scheduling, self-healing controllers, service discovery, controlled rollouts, resource management, and scaling.

---

## Q4. What is the difference between Kubernetes and Docker?

### 1. English Definition

Docker is a platform and toolset commonly used to build, package, and run containers. Kubernetes is a container orchestration platform that schedules and manages containerized workloads across a cluster.

### 2. Hindi Definition

Docker ka use commonly container image build aur container run karne ke liye hota hai. Kubernetes ka use cluster mein containerized applications ko deploy, scale aur manage karne ke liye hota hai.

### 3. Hinglish Explanation

Docker aur Kubernetes direct alternatives nahi hain; dono alag problems solve karte hain.

- Dockerfile se image build kar sakte ho.
- Container runtime image se container run karta hai.
- Kubernetes Pods aur controllers ke through workloads manage karta hai.
- Kubernetes cluster mein container runtime ke liye containerd jaise runtime use ho sakte hain; Kubernetes ko Docker Engine ki requirement nahi hai.

MERN example: aap Node.js backend ki image Docker se build karte ho, image registry mein push karte ho, phir Kubernetes Deployment us image ko Pods mein run karwata hai.

### 4. Practical Example / Code

Build and push an image (replace the image name with your registry path):

```bash
docker build -t registry.example.com/my-backend:1.0 .
docker push registry.example.com/my-backend:1.0
```

Reference that image in a Kubernetes Deployment:

```yaml
containers:
  - name: backend
    image: registry.example.com/my-backend:1.0
    ports:
      - containerPort: 5000
```

### 5. Architecture Diagram

```text
Application Source
       |
       v
Dockerfile / Build Tool
       |
       v
Container Image
       |
       v
Container Registry
       |
       v
Kubernetes Deployment
       |
       v
Pods on Cluster Nodes
```

### 6. Practical Commands

```bash
docker build -t my-backend:1.0 .
docker image ls
kubectl get deployments
kubectl get pods
```

The local image built on your laptop is not automatically available to a remote cluster. Push it to a registry the cluster can access, or use an appropriate local-cluster image-loading workflow.

### 7. Summary Table

| Feature | Docker | Kubernetes |
|---|---|---|
| Main purpose | Build/package/run containers | Orchestrate workloads across a cluster |
| Image build | Commonly supported | Does not build images by itself |
| Scaling | Can run multiple containers manually or via other tools | Declarative replicas and autoscaling options |
| Recovery | Depends on Docker settings and external tooling | Controllers reconcile workload state |
| Networking | Container networks and port publishing | Pods, Services, DNS, and cluster networking |
| Typical use together | Build/publish image | Run and manage image as Pods |

**Interview-ready summary:** Docker is commonly used to build and run container images, while Kubernetes orchestrates containerized workloads across a cluster. In many workflows, developers build and publish images first, then Kubernetes runs them through Deployments and Pods.

---

## Q5. What is a container?

### 1. English Definition

A container is an isolated runtime environment for an application process and its dependencies. On Linux, containers use operating-system features to isolate processes while sharing the host kernel.

### 2. Hindi Definition

Container ek isolated runtime environment hota hai jisme application process aur uski required dependencies run hoti hain. Linux par containers host OS ka kernel share karte hain.

### 3. Hinglish Explanation

Maan lo Node.js backend ko uske runtime aur packages ke saath ek image mein package kiya gaya. Us image ko run karne par container create hota hai. Container application ko host par doosre processes se isolate karne mein help karta hai.

Container aur VM same nahi hote. VM mein apna guest OS hota hai; Linux container host kernel share karta hai. Container ke andar write kiya gaya data container remove hone par lose ho sakta hai, isliye important data ke liye persistent volume ya external database use karte hain.

Kubernetes mein container directly top-level workload object nahi hota; container Pod ke andar define hota hai.

### 4. Practical Example / Code

A minimal container definition inside a Pod:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx
      image: nginx:1.27
      ports:
        - containerPort: 80
```

### 5. Architecture Diagram

```text
Kubernetes Pod
+----------------------------+
| Container                  |
|  Application Process       |
|  Runtime / Libraries       |
+----------------------------+
| Container Runtime          |
+----------------------------+
| Worker Node OS / Kernel    |
+----------------------------+
```

### 6. Practical Commands

```bash
kubectl apply -f nginx-pod.yaml
kubectl get pod nginx-pod
kubectl logs nginx-pod
kubectl delete pod nginx-pod
```

A standalone Pod is useful for learning, but a Deployment is generally preferred for a stateless application because it manages replacement Pods and rollouts.

### 7. Summary Table

| Term | Meaning |
|---|---|
| Container | Isolated application runtime |
| Image | Template used to create a container |
| Pod | Kubernetes unit that hosts one or more containers |
| Persistence | Use volumes or external storage for data that must survive replacement |
| Container runtime | Software that runs containers on a node |

**Interview-ready summary:** A container is an isolated runtime environment that packages an application process with its runtime dependencies. In Kubernetes, containers run inside Pods, which are scheduled onto cluster nodes.

---

## Q6. What is the difference between Kubernetes and Docker Compose?

### 1. English Definition

Docker Compose is a tool for defining and running multi-container applications, commonly on one Docker host. Kubernetes is a cluster orchestration platform with declarative workload management, scheduling, service discovery, and scaling capabilities across nodes.

### 2. Hindi Definition

Docker Compose ek YAML file ke through multiple containers aur unke networks/volumes ko define aur run karne ka tool hai. Kubernetes cluster mein workloads ko schedule aur manage karta hai aur larger production environments ke liye orchestration features deta hai.

### 3. Hinglish Explanation

MERN project ka example lo. Docker Compose mein aap React frontend, Node.js backend aur MongoDB services ko ek `compose.yaml` file mein define karke saath run kar sakte ho. Yeh local development aur simple deployments ke liye convenient hai.

Kubernetes mein aap commonly frontend/backend ke liye Deployments, internal communication ke liye Services, configuration ke liye ConfigMaps/Secrets aur external traffic ke liye Ingress ya LoadBalancer use karte ho.

Kubernetes automatically har problem solve nahi karta. Production setup ke liye monitoring, security, storage, resource sizing aur operational practices phir bhi chahiye.

### 4. Practical Example / Code

Docker Compose example:

```yaml
services:
  backend:
    build: ./backend
    ports:
      - "5000:5000"
    environment:
      MONGO_URI: mongodb://mongodb:27017/appdb
    depends_on:
      - mongodb

  mongodb:
    image: mongo:7
    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
```

Equivalent Kubernetes setup usually uses separate manifests for a backend Deployment, backend Service, MongoDB StatefulSet or appropriate database service, and persistent storage. For production, a managed database may be preferable.

### 5. Architecture Diagram

```text
Docker Compose
compose.yaml
     |
     +---- backend container
     +---- frontend container
     +---- database container
     |
Usually one Docker host

Kubernetes
Manifests / API
     |
     +---- Control Plane / Scheduler
                 |
        +--------+--------+
        |                 |
      Node 1            Node 2
      Pods              Pods
                         /
             Services
```

### 6. Practical Commands

Docker Compose:

```bash
docker compose up -d
docker compose ps
docker compose logs
docker compose down
```

Kubernetes:

```bash
kubectl apply -f k8s/
kubectl get deployments,pods,services
kubectl rollout status deployment/backend
```

### 7. Summary Table

| Feature | Docker Compose | Kubernetes |
|---|---|---|
| Typical use | Local development and multi-container apps | Cluster orchestration and production workloads |
| Configuration | Compose YAML | Kubernetes manifests / API objects |
| Scheduling across nodes | Not its primary role | Built-in scheduler |
| Scaling | Can scale service containers, with limitations depending on setup | Replica management and autoscaling options |
| Self-healing | Restart policies for containers | Controllers reconcile desired workload state |
| Learning/operations | Usually simpler to start | More concepts and cluster operations |

**Interview-ready summary:** Docker Compose is simpler for defining and running a multi-container application, especially in local development. Kubernetes provides cluster-level scheduling, desired-state reconciliation, service discovery, and richer rollout and scaling mechanisms.

---

## Q7. What is Kubernetes architecture?

### 1. English Definition

Kubernetes architecture consists of a control plane that exposes the Kubernetes API and manages cluster state, plus worker nodes that run Pods through a container runtime.

### 2. Hindi Definition

Kubernetes architecture mein Control Plane cluster ko manage karta hai, aur Worker Nodes par application ke Pods run hote hain. Dono API aur cluster mechanisms ke through coordinate karte hain.

### 3. Hinglish Explanation

Control Plane ko cluster ka management layer samjho. Aap `kubectl apply` se YAML submit karte ho. API Server request validate karke cluster state store karta hai. Scheduler un Pods ke liye suitable node choose karta hai jinhe abhi assign nahi kiya gaya. Controllers desired state aur actual state compare karke changes reconcile karte hain.

Worker Node par:
- **Kubelet** node par assigned Pods ko manage karta hai.
- **Container runtime** containers run karta hai.
- **kube-proxy** commonly Service networking rules implement karta hai, although some cluster networking implementations replace this role.

### 4. Practical Example / Code

See node and control-plane related resources:

```bash
kubectl get nodes -o wide
kubectl get pods -A
kubectl get componentstatuses
```

Note: `kubectl get componentstatuses` is deprecated/removed in modern Kubernetes releases and is not a reliable general health check. Prefer the cluster provider's health tooling, node conditions, and relevant system Pods/logs.

### 5. Architecture Diagram

```text
                kubectl / API Clients
                        |
                        v
              +---------------------+
              |    Control Plane    |
              |---------------------|
              | kube-apiserver      |
              | etcd                |
              | kube-scheduler      |
              | controller-manager  |
              | cloud-controller*   |
              +---------------------+
                        |
                  Cluster API
             +----------+----------+
             |                     |
             v                     v
     +---------------+     +---------------+
     | Worker Node A |     | Worker Node B |
     | kubelet       |     | kubelet       |
     | runtime       |     | runtime       |
     | Pods          |     | Pods          |
     +---------------+     +---------------+

*cloud-controller-manager is used in applicable cloud integrations.
```

### 6. Practical Commands

```bash
kubectl cluster-info
kubectl get nodes
kubectl describe node <node-name>
kubectl get pods -n kube-system
```

Replace `<node-name>` with an actual node name. Access to control-plane components and system Pods may differ on a managed Kubernetes service.

### 7. Summary Table

| Component | Role |
|---|---|
| API Server | Entry point for Kubernetes API requests |
| etcd | Stores cluster state |
| Scheduler | Selects nodes for unscheduled Pods |
| Controller Manager | Runs controllers that reconcile desired state |
| Kubelet | Manages Pods assigned to a worker node |
| Container runtime | Runs containers |
| kube-proxy | Commonly implements Service networking rules |

**Interview-ready summary:** Kubernetes has a control plane for API access, state storage, scheduling, and reconciliation, while worker nodes run the application Pods. The components work together to move the cluster toward the declared desired state.

---

## Q8. What is a Kubernetes cluster?

### 1. English Definition

A Kubernetes cluster is a set of machines, called nodes, managed by Kubernetes to run containerized workloads. It includes the control plane and the worker capacity where Pods execute.

### 2. Hindi Definition

Kubernetes cluster machines ka group hota hai jise Kubernetes ek unit ki tarah manage karta hai. Ismein Control Plane aur workload run karne wale Worker Nodes hote hain.

### 3. Hinglish Explanation

Maan lo aapke paas 3 worker machines hain. Kubernetes unhe ek cluster ke roop mein manage kar sakta hai. Aap Deployment submit karte ho aur Scheduler available resources, constraints aur policies dekhkar Pods ko eligible nodes par place karta hai.

Cluster local laptop par Minikube/kind se bhi ho sakta hai, ya cloud mein Amazon EKS jaise managed service par. Managed service mein provider kuch control-plane responsibilities handle kar sakta hai.

### 4. Practical Example / Code

List cluster nodes:

```bash
kubectl get nodes
kubectl get nodes -o wide
```

Example output shape (actual values vary):

```text
NAME          STATUS   ROLES    AGE   VERSION
worker-a      Ready    <none>   ...   v1.xx.x
worker-b      Ready    <none>   ...   v1.xx.x
```

### 5. Architecture Diagram

```text
          Kubernetes Cluster
+----------------------------------+
| Control Plane                    |
| API Server / Scheduler / etcd    |
+----------------------------------+
| Worker Node 1 | Worker Node 2    |
| Pods          | Pods             |
+----------------------------------+
| Worker Node 3                    |
| Pods                             |
+----------------------------------+
```

### 6. Practical Commands

```bash
kubectl cluster-info
kubectl get nodes
kubectl get namespaces
kubectl get pods -A
```

### 7. Summary Table

| Term | Meaning |
|---|---|
| Cluster | Kubernetes-managed set of nodes |
| Control Plane | Manages API and cluster state |
| Node | Machine participating in the cluster |
| Pod | Workload unit scheduled to a node |
| kubectl | CLI used to interact with the Kubernetes API |

**Interview-ready summary:** A Kubernetes cluster is a group of nodes managed as one system. The control plane maintains cluster state and schedules workloads, while worker nodes provide capacity to run Pods.

---

## Q9. What is a node?

### 1. English Definition

A Kubernetes node is a physical or virtual machine that participates in a cluster and provides resources to run Pods. A node runs node-level components such as kubelet and a container runtime.

### 2. Hindi Definition

Kubernetes node ek physical ya virtual machine hoti hai jo cluster ka hissa hoti hai aur Pods ko run karne ke liye CPU, memory aur other resources provide karti hai.

### 3. Hinglish Explanation

Node ko ek server samjho jahan application ke Pods run hote hain. Scheduler decide karta hai ki Pod kis eligible node par place ho. Node par kubelet API Server ke saath communicate karke assigned Pods ki desired configuration apply karwata hai.

Agar node NotReady ho jaye, toh us node par running workloads impact ho sakte hain. Kubernetes workload controllers replacement Pods create kar sakte hain, lekin recovery available capacity, storage, scheduling rules aur failure conditions par depend karti hai.

### 4. Practical Example / Code

Inspect nodes and resource capacity:

```bash
kubectl get nodes -o wide
kubectl describe node <node-name>
kubectl top nodes
```

`kubectl top nodes` ke liye Metrics Server ya compatible metrics provider configured hona chahiye.

### 5. Architecture Diagram

```text
+-------------------------------+
| Kubernetes Worker Node        |
|-------------------------------|
| kubelet                       |
| Container Runtime             |
| Networking components         |
|-------------------------------|
| Pod A       | Pod B           |
| App         | App             |
| CPU / Memory / Storage use    |
+-------------------------------+
```

### 6. Practical Commands

```bash
kubectl get nodes
kubectl describe node <node-name>
kubectl get pods -o wide
kubectl top nodes
```

### 7. Summary Table

| Node item | Purpose |
|---|---|
| CPU and memory | Resources used by Pods |
| kubelet | Manages Pods assigned to the node |
| Container runtime | Runs containers |
| Node conditions | Report readiness and other node health information |
| Scheduler | Chooses eligible nodes for unscheduled Pods |

**Interview-ready summary:** A node is a physical or virtual machine in a Kubernetes cluster that runs Pods. It provides compute resources and runs components such as kubelet and a container runtime.

---

## Q10. What is a master node / control plane?

### 1. English Definition

The Kubernetes control plane is the set of components responsible for exposing the Kubernetes API, storing cluster state, scheduling workloads, and reconciling resources toward their desired state. “Master node” is an older term; “control plane” is preferred.

### 2. Hindi Definition

Control Plane Kubernetes cluster ka management layer hai. Yeh API requests handle karta hai, cluster state store karta hai, Pods ke liye node select karta hai aur controllers ke through desired state maintain karne ki koshish karta hai.

### 3. Hinglish Explanation

Jab aap `kubectl apply -f deployment.yaml` chalate ho, toh request Kubernetes API Server tak jaati hai. API Server configuration validate karta hai aur state update hoti hai. Scheduler un Pods ke liye node select karta hai jinke paas abhi node assignment nahi hai. Controller Manager desired replicas aur actual Pods ko compare karta hai.

Managed Kubernetes, jaise EKS, mein control plane provider manage kar sakta hai. Iska matlab yeh nahi ki application ke worker nodes, manifests, permissions aur workload configuration automatically manage ho jaate hain.

### 4. Practical Example / Code

Create a Deployment through the API:

```bash
kubectl apply -f nginx-deployment.yaml
kubectl get deployment nginx-deployment
kubectl describe deployment nginx-deployment
kubectl get events --sort-by=.metadata.creationTimestamp
```

### 5. Architecture Diagram

```text
            kubectl apply -f app.yaml
                       |
                       v
              +----------------+
              | API Server     |
              +----------------+
                |            |
                v            v
             etcd        Controllers
                             |
                             v
                         Scheduler
                             |
                             v
                       Worker Node
                             |
                             v
                            Pod
```

The diagram is simplified: scheduling, persistence, and reconciliation involve API interactions and may proceed asynchronously.

### 6. Practical Commands

```bash
kubectl cluster-info
kubectl get nodes
kubectl get pods -n kube-system
kubectl get events --sort-by=.metadata.creationTimestamp
```

On managed services, control-plane processes may not appear as ordinary Pods you can inspect.

### 7. Summary Table

| Control-plane component | Main responsibility |
|---|---|
| kube-apiserver | Kubernetes API endpoint |
| etcd | Persistent cluster state store |
| kube-scheduler | Places unscheduled Pods on eligible nodes |
| kube-controller-manager | Runs reconciliation controllers |
| cloud-controller-manager | Integrates with cloud infrastructure when applicable |

**Interview-ready summary:** The control plane manages the Kubernetes cluster through the API Server, etcd, Scheduler, and controllers. It accepts desired configuration, stores cluster state, assigns Pods to nodes, and continuously reconciles actual resources toward the desired state.
