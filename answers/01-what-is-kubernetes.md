# 1. What Is Kubernetes?

## 1. English Definition

**Kubernetes (K8s) is an open-source container orchestration platform that automates the deployment, scaling, networking, and management of containerized applications across a cluster of machines.**

It helps keep applications running in the desired state. For example, if you configure a Deployment to run three replicas of an application and one Pod fails, Kubernetes works to create a replacement.

> **Interview tip:** Kubernetes does not replace Docker as a tool for building images. It orchestrates containerized workloads. Kubernetes commonly uses container runtimes such as containerd to run containers.

## 2. Hindi Definition

**Kubernetes एक open-source container orchestration platform है, जो कई machines के cluster में containerized applications को deploy करने, उनकी संख्या बढ़ाने या घटाने, networking करने और उन्हें manage करने के काम को automate करता है।**

अगर application का कोई Pod fail हो जाता है, तो Kubernetes desired state बनाए रखने की कोशिश करता है और ज़रूरत पड़ने पर नया Pod बनाता है।

## 3. Hinglish Explanation

Simple words mein, maan lo aapki MERN application mein Node.js backend hai. Aap chahte ho ki backend ke 3 instances hamesha running rahein.

Kubernetes ko aap bata dete ho: **“Mujhe backend ke 3 replicas chahiye.”**

Phir Kubernetes:
- Application ko cluster ke worker nodes par run karwata hai.
- Pods ko schedule karta hai.
- Pod fail hone par replacement create karne ki koshish karta hai.
- Traffic ko Service ke through available Pods tak route karta hai.
- Configuration ke according replicas ko scale kar sakta hai.

Aapko har failed Pod ko manually recreate karne ki zaroorat nahi hoti. Kubernetes controllers continuously actual state ko desired state ke saath match karne ki koshish karte hain.

**Important:** Kubernetes khud application ka business logic nahi chalata aur na hi Docker image banata hai. Aap image build karte ho, aur Kubernetes us image se application ke containers ko manage karta hai.

## 4. Practical Example / Code

Example: NGINX web server ke 3 replicas run karna.

Create a file named `nginx-deployment.yaml`:

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

### What does this YAML mean?

| YAML field | Meaning |
|---|---|
| `kind: Deployment` | Kubernetes should manage the application through a Deployment. |
| `replicas: 3` | The desired number of Pods is three. |
| `selector.matchLabels` | Identifies the Pods managed by this Deployment. |
| `template` | Defines how each Pod should be created. |
| `image: nginx:1.27` | The container image to run. |
| `containerPort: 80` | Documents the port the container listens on; it does not by itself expose the app outside the cluster. |

## 5. Architecture Diagram

This simplified diagram shows how you interact with Kubernetes and how it runs an application.

```text
              Developer / kubectl
                       |
                       v
             +-------------------+
             |   Control Plane   |
             |-------------------|
             | API Server        |
             | Scheduler         |
             | Controllers       |
             | etcd              |
             +-------------------+
                       |
              schedules / manages
                       |
          +------------+------------+
          |                         |
          v                         v
+--------------------+   +--------------------+
|    Worker Node 1   |   |    Worker Node 2   |
|--------------------|   |--------------------|
| Kubelet            |   | Kubelet            |
| Container Runtime  |   | Container Runtime  |
| Pod: NGINX         |   | Pod: NGINX         |
+--------------------+   +--------------------+
                                   /
           ---- Service routing --/
```

**Component overview:**
- **API Server:** Entry point for Kubernetes API requests.
- **Scheduler:** Selects a suitable worker node for a Pod that needs scheduling.
- **Controllers:** Reconcile the actual state toward the desired state.
- **etcd:** Stores Kubernetes cluster state and configuration data.
- **Worker node:** Runs Pods.
- **Kubelet:** Makes sure the Pods assigned to its node are handled as specified.
- **Container runtime:** Runs containers.
- **Service:** Provides a stable network endpoint for a group of Pods.

## 6. Practical Commands / Configuration

Run these commands from a terminal configured to access your Kubernetes cluster.

### Apply the Deployment

```bash
kubectl apply -f nginx-deployment.yaml
```

### Check the Deployment and Pods

```bash
kubectl get deployments
kubectl get pods -o wide
```

### Inspect the Deployment

```bash
kubectl describe deployment nginx-deployment
```

### Scale from 3 replicas to 5

```bash
kubectl scale deployment nginx-deployment --replicas=5
kubectl get pods
```

### Delete the example Deployment

```bash
kubectl delete -f nginx-deployment.yaml
```

**Note:** The Deployment above does not expose NGINX outside the cluster. To access it through a stable endpoint, create a Kubernetes Service (for example, a ClusterIP Service for internal access, or an appropriate external-access setup).

## 7. Summary Table

| Topic | Quick revision |
|---|---|
| What is Kubernetes? | An open-source container orchestration platform. |
| Main purpose | Automates deployment, scaling, and management of containerized applications. |
| Where does it run workloads? | In Pods scheduled on cluster worker nodes. |
| What is a Pod? | The smallest deployable unit in Kubernetes; it can contain one or more containers. |
| What if a Pod fails? | Controllers can create replacement Pods to move toward the desired state. |
| Does Kubernetes build Docker images? | No. Build and publish an image separately, then reference it in Kubernetes configuration. |
| How do you define a workload? | Commonly with declarative YAML manifests, such as a Deployment. |
| How do you interact with a cluster? | Often with `kubectl` and the Kubernetes API. |

## 8. Interview-Ready Answer

“Kubernetes is an open-source container orchestration platform used to automate the deployment, scaling, and management of containerized applications. It runs workloads in Pods across a cluster of machines and uses controllers to maintain the desired state. For example, if I configure a Deployment with three replicas, Kubernetes works to keep three Pods running and can replace a failed Pod.”

### One-line Hinglish Revision

**Kubernetes containers ko cluster mein deploy, scale aur manage karta hai, aur desired state maintain karne ki koshish karta hai.**
