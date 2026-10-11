# 1. What is Kubernetes?

## 1. English Definition

**Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, networking, and management of containerized applications.**

## 2. Hindi Definition

Kubernetes ek open-source platform hai jo containers mein chalne wali applications ko automatically deploy, scale aur manage karta hai.

## 3. Hinglish Explanation — MERN Stack Example

Maan lo aapne ek MERN Stack e-commerce application banayi hai:

- **React:** Frontend
- **Node.js + Express.js:** Backend API
- **MongoDB:** Database

Aapne React aur Node.js applications ki Docker images bana kar containers mein run kar di. Ab production mein users bahut zyada aa sakte hain, containers crash ho sakte hain aur application ko multiple servers par chalana pad sakta hai.

Yahan Kubernetes kaam aata hai. Kubernetes containers ko manage karne, application ki desired number of replicas maintain karne aur workloads ko cluster ke nodes par run karwane mein help karta hai.

### Kubernetes kya-kya karta hai?

1. **Deployment:** Application ko cluster par run karwata hai aur desired number of replicas maintain karne mein help karta hai.
2. **Scaling:** Traffic badhne par backend replicas 3 se 5 kar sakte hain.
3. **Self-healing:** Agar koi Pod fail ho jaye, toh Kubernetes uski jagah replacement Pod create kar sakta hai.
4. **Networking:** Kubernetes Services Pods ko stable network access aur traffic distribution provide karti hain.

## 4. Practical Example — Node.js Backend

Maan lo aapki Docker image available hai:

`your-dockerhub-username/mern-backend:1.0`

Kubernetes mein backend ke 3 replicas run karne ke liye Deployment YAML bana sakte ho.

### `backend-deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: mern-backend

spec:
  replicas: 3

  selector:
    matchLabels:
      app: mern-backend

  template:
    metadata:
      labels:
        app: mern-backend

    spec:
      containers:
        - name: backend
          image: your-dockerhub-username/mern-backend:1.0
          ports:
            - containerPort: 5000
```

Is configuration mein:

- `replicas: 3` — Kubernetes 3 Pods maintain karne ki koshish karega.
- `image` — Docker Hub par available backend image.
- `containerPort: 5000` — container ke andar Node.js application ka port.
- `selector` aur `labels` — Deployment ko apne Pods identify karne mein help karte hain.

**Note:** Image name ko apni actual Docker image se replace karein. Kubernetes cluster aur image pull access pehle se configured hone chahiye.

## 5. Practical Commands

Deployment create/apply karne ke liye:

```bash
kubectl apply -f backend-deployment.yaml
```

Pods check karne ke liye:

```bash
kubectl get pods
```

Deployment check karne ke liye:

```bash
kubectl get deployments
```

Backend replicas ko 3 se 5 karne ke liye:

```bash
kubectl scale deployment mern-backend --replicas=5
```

Kubernetes cluster ke nodes check karne ke liye:

```bash
kubectl get nodes
```

## 6. Kubernetes Architecture

```text
                 CONTROL PLANE
      +----------------------------------+
      | API Server                       |
      | Scheduler                        |
      | Controller Manager               |
      | etcd (cluster state data)        |
      +----------------+-----------------+
                       |
              manages workloads
                       |
        +--------------+--------------+
        |                             |
+-------v----------+        +---------v--------+
| Worker Node 1    |        | Worker Node 2    |
|                  |        |                  |
|  +------------+  |        |  +------------+  |
|  | Pod A      |  |        |  | Pod C      |  |
|  | Node.js API|  |        |  | Node.js API|  |
|  +------------+  |        |  +------------+  |
|  +------------+  |        |  +------------+  |
|  | Pod B      |  |        |  | Pod D      |  |
|  +------------+  |        |  +------------+  |
+------------------+        +------------------+
```

- **Control Plane:** Cluster ko manage karta hai aur desired state maintain karne ke liye decisions leta hai.
- **Worker Nodes:** In par application ke Pods run hote hain.
- **Pod:** Kubernetes ki smallest deployable unit hai; ismein ek ya zyada containers ho sakte hain.
- **Service:** Pods ko stable network access deti hai aur configured traffic distribution mein help karti hai.

Chhote local clusters mein Control Plane aur workloads ka setup alag bhi ho sakta hai.

## 7. Summary Table

| Term | Simple meaning |
|---|---|
| Kubernetes | Containers ko orchestrate aur manage karta hai |
| Cluster | Kubernetes environment |
| Node | Cluster ki machine |
| Pod | Kubernetes ki smallest deployable unit |
| Container | Application run karne ka isolated environment |
| Deployment | Pods aur unke replicas manage karta hai |
| Service | Pods ko stable network access deti hai |
| Scaling | Application replicas ki sankhya badhana ya ghatana |

**Yaad rakhne wali baat:** Docker containers banane aur run karne mein help karta hai; Kubernetes multiple containers aur Pods ko production environment mein deploy, scale aur manage karne mein help karta hai.
