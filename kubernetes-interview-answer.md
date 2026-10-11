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


---

# 2. Why Do We Need Kubernetes?

## 1. English Definition

**We need Kubernetes to automate the deployment, scaling, traffic distribution, and management of containerized applications so they can remain reliable and handle changing workloads.**

## 2. Hindi Definition

Humein Kubernetes ki zaroorat isliye hoti hai taaki hum apni containerized applications ko automatically deploy, scale aur manage kar sakein, aur application ko reliable tareeke se run kar sakein.

## 3. Hinglish Explanation — MERN Stack Example

Maan lo aapne MERN Stack mein ek e-commerce website banayi hai:

- **React:** Frontend
- **Node.js + Express.js:** Backend API
- **MongoDB:** Database

Aapne Docker ki help se frontend aur backend ke containers bana liye. Shuru mein application par 100 users aate hain, toh application easily chalti hai. Lekin baad mein 10,000 users aa jaate hain, ya backend ka koi Pod crash ho jaata hai. Ab aapko replicas manage karne, failed Pods replace karne aur requests ko available instances tak route karne ki zaroorat hoti hai.

### Kubernetes ke bina kya problems hongi?

1. **Container/Pod failure:** Failed instance ko replace ya restart karne ka arrangement karna padega.
2. **Traffic increase:** Backend ke additional instances run karne aur traffic distribute karne ka arrangement chahiye.
3. **Multiple machines:** Containers ko machines par schedule karna aur resources manage karna complex ho sakta hai.
4. **Manual operations:** Deployments, updates, monitoring aur replica count ko manually manage karne ka effort badhta hai.

### Kubernetes in problems ko kaise solve karta hai?

1. **Self-healing:** Deployment jaise workload controllers failed Pod ko replace kar sakte hain, taaki desired replica count maintain rahe.
2. **Scaling:** Replicas ko manually scale kar sakte hain, ya Horizontal Pod Autoscaler (HPA) ke through supported metrics ke basis par automatically adjust kar sakte hain.
3. **Service networking:** Kubernetes Service traffic ko available backend Pods tak route karne mein help karti hai.
4. **Rollouts:** Deployment application updates ko controlled rolling updates ke through release kar sakta hai.

## 4. Practical Example — Manual Scaling

Maan lo aapke backend Deployment mein abhi 3 replicas hain.

```bash
kubectl scale deployment mern-backend --replicas=5
kubectl get deployments
kubectl get pods
```

Isse desired replica count 3 se 5 ho jaata hai. Kubernetes 5 Pods maintain karne ki koshish karega, agar cluster resources aur application configuration allow karein.

## 5. Horizontal Scaling vs Vertical Scaling

| Type | Meaning | Kubernetes example |
|---|---|---|
| Horizontal scaling | Pods/instances ki count badhana ya ghatana | 3 backend Pods se 5 backend Pods |
| Vertical scaling | Ek Pod/container ko zyada ya kam CPU/memory dena | CPU request/limit ya memory request/limit badalna |

**Easy way to remember:** Horizontal = more/fewer instances. Vertical = an instance ko more/less resources.

## 6. Horizontal Pod Autoscaler (HPA)

**English definition:** Horizontal Pod Autoscaler automatically adjusts the number of Pod replicas in a workload, such as a Deployment, based on observed metrics.

**Hinglish explanation:** HPA current metrics ko target ke saath compare karta hai aur zaroorat ke hisaab se backend Pods ki count badhata ya ghatata hai. For example, CPU utilization target se consistently zyada ho, toh HPA replicas increase kar sakta hai; load kam hone par replicas reduce bhi kar sakta hai, configured minimum aur maximum ke beech.

### HPA ka flow

```text
Incoming traffic increases
          |
          v
Backend Pods ka CPU usage increase hota hai
          |
          v
Metrics Server metrics provide karta hai
          |
          v
Horizontal Pod Autoscaler target se compare karta hai
          |
          v
Deployment ke replicas increase ho sakte hain
          |
          v
Kubernetes additional Pods schedule karta hai
```

### Step 1: Deployment mein CPU request configure karein

HPA ke CPU utilization target ke liye container par CPU request set honi chahiye. Deployment ke container section ka relevant example:

```yaml
resources:
  requests:
    cpu: "100m"
  limits:
    cpu: "500m"
```

Isse existing Deployment YAML ke container definition ke andar add karein, `ports` ke saath same indentation level par.

### Step 2: HPA configuration banayein

File: `backend-hpa.yaml`

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler

metadata:
  name: mern-backend-hpa

spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: mern-backend

  minReplicas: 3
  maxReplicas: 10

  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70
```

Is configuration ka meaning:

- `scaleTargetRef`: HPA, `mern-backend` Deployment ko scale karega.
- `minReplicas: 3`: replicas 3 se neeche nahi jaayenge.
- `maxReplicas: 10`: replicas 10 se zyada nahi honge.
- `averageUtilization: 70`: target average CPU utilization 70% hai, jo configured CPU requests ke relative measure hota hai.

### Step 3: HPA apply karein aur verify karein

```bash
kubectl apply -f backend-deployment.yaml
kubectl apply -f backend-hpa.yaml
kubectl get hpa
kubectl describe hpa mern-backend-hpa
kubectl get pods
```

**Important prerequisites:** Cluster mein Metrics Server ya equivalent supported resource metrics API available honi chahiye, aur containers ki CPU requests configured honi chahiye. HPA load aate hi instant scaling ki guarantee nahi deta; metrics collection, scaling behavior, scheduling aur available cluster resources ka effect hota hai. HPA replica count manage karta hai; cluster mein worker nodes ki capacity badhana alag concern hai, jiske liye cluster autoscaling ki zaroorat ho sakti hai.

## 7. Summary Table

| Problem / need | Kubernetes feature | Benefit |
|---|---|---|
| Pod fail ho gaya | Workload controller / self-healing | Replacement Pod create kar sakta hai |
| Traffic badh gaya | Manual scaling or HPA | Backend replicas increase kar sakte hain |
| Traffic kam ho gaya | HPA | Configured minimum tak replicas reduce kar sakta hai |
| Pods tak traffic pahunchana hai | Service | Stable endpoint aur traffic routing |
| Application update karni hai | Deployment rollout | Controlled updates |
| Resources distribute karne hain | Scheduler | Pods ko suitable nodes par place karta hai |

Kubernetes operations ko automate karta hai, lekin reliable production setup ke liye health checks, resource requests/limits, monitoring, security aur application-level error handling bhi important hain.
