# Kubernetes Interview Questions — Topic-wise (225 Questions)

A topic-wise Kubernetes interview preparation roadmap for developers, with a focus on MERN stack, Docker, AWS, and practical troubleshooting. Questions are in English so they can be practised directly for interviews.

> Study one topic at a time. Practise commands in a test cluster (such as kind or Minikube) before using them in production. Answers can be added in English definition + Hinglish explanation + practical YAML/command example format.

## 1. Kubernetes Fundamentals
1. What is Kubernetes?
2. Why do we need Kubernetes?
3. What problems does Kubernetes solve?
4. What are the main benefits of Kubernetes?
5. What is container orchestration?
6. What is the difference between Docker and Kubernetes?
7. What is the difference between Docker Compose and Kubernetes?
8. What is a Kubernetes cluster?
9. What is a node in Kubernetes?
10. What is the difference between a control plane node and a worker node?
11. What is a Pod?
12. What is the difference between a container and a Pod?
13. What is a Namespace?
14. What is a label in Kubernetes?
15. What is a selector in Kubernetes?

## 2. Kubernetes Architecture
16. What are the main Kubernetes control plane components?
17. What does the kube-apiserver do?
18. What is etcd and what data does it store?
19. What does the kube-scheduler do?
20. What does the kube-controller-manager do?
21. What is the cloud-controller-manager?
22. What are the main worker node components?
23. What does kubelet do?
24. What does kube-proxy do?
25. What is a container runtime?
26. How does Kubernetes use the Container Runtime Interface (CRI)?
27. How does Kubernetes process a Deployment creation request?
28. How does the scheduler select a node for a Pod?
29. How do controllers maintain the desired state?
30. What happens if the API server or etcd becomes unavailable?

## 3. Pods and Containers
31. What is a Pod and why is it the smallest deployable Kubernetes unit?
32. When would you run multiple containers in one Pod?
33. What is a sidecar container?
34. What is an init container?
35. What is the Pod lifecycle?
36. What do Pending, Running, Succeeded, Failed, and Unknown mean?
37. What is a Pod restart policy?
38. What is CrashLoopBackOff?
39. What is ImagePullBackOff?
40. What is the difference between a Pod phase and a container state?
41. How do you view logs from a Pod?
42. How do you view logs from a previous crashed container?
43. How do you execute a command inside a running container?
44. How do you inspect a Pod's IP and node?
45. What happens to a standalone Pod when its node fails?

## 4. Deployments and ReplicaSets
46. What is a Deployment?
47. What is a ReplicaSet?
48. What is the difference between a Deployment, ReplicaSet, and Pod?
49. Why are Deployments preferred over creating Pods directly?
50. How do you define replicas in a Deployment?
51. How do labels and selectors connect a Deployment to its Pods?
52. What is a rolling update?
53. How do you roll back a Deployment?
54. What is the difference between RollingUpdate and Recreate strategies?
55. What are maxSurge and maxUnavailable?
56. How do you scale a Deployment manually?
57. What does kubectl rollout status do?
58. What does kubectl rollout history do?
59. What happens if a Pod managed by a Deployment is deleted?
60. How do you update a container image in a Deployment?

## 5. Services and Networking
61. Why does Kubernetes need Services?
62. What is a Kubernetes Service?
63. What are the main Service types?
64. What is a ClusterIP Service?
65. What is a NodePort Service?
66. What is a LoadBalancer Service?
67. What is an ExternalName Service?
68. What is the difference between ClusterIP, NodePort, and LoadBalancer?
69. How does a Service select backend Pods?
70. What are EndpointSlices?
71. How does one Pod communicate with another Pod?
72. How does Kubernetes DNS work?
73. What is a fully qualified service DNS name?
74. Why should applications generally use Service DNS instead of Pod IPs?
75. How would you debug a Service that has no endpoints?

## 6. ConfigMaps, Secrets, and Environment Variables
76. What is a ConfigMap?
77. What is a Secret?
78. What is the difference between a ConfigMap and a Secret?
79. How do you inject environment variables into a container?
80. How do you expose ConfigMap values as environment variables?
81. How do you mount a Secret as files?
82. Does updating a ConfigMap automatically restart a Pod?
83. Are Kubernetes Secret values encrypted by default in etcd?
84. How do you improve Secret security in production?
85. How would you manage Node.js configuration across development, staging, and production?

## 7. Volumes and Persistent Storage
86. What is a Kubernetes Volume?
87. What is the difference between ephemeral and persistent storage?
88. What is emptyDir?
89. What is a PersistentVolume (PV)?
90. What is a PersistentVolumeClaim (PVC)?
91. What is the difference between PV and PVC?
92. What is a StorageClass?
93. What is dynamic volume provisioning?
94. What are access modes such as ReadWriteOnce and ReadWriteMany?
95. What happens to persistent data when a Pod is deleted?
96. What is a volume mount?
97. How would you provide persistent storage to a database workload?

## 8. Ingress and External Traffic
98. What is Kubernetes Ingress?
99. What is an Ingress Controller?
100. What is the difference between an Ingress resource and an Ingress Controller?
101. How does Ingress differ from a Service of type LoadBalancer?
102. What are host-based and path-based routing?
103. How do you route traffic for a custom domain to an application?
104. How do you configure HTTPS/TLS for an application?
105. What is the role of DNS in exposing a Kubernetes application?
106. How would you troubleshoot an application that is not reachable from outside the cluster?
107. Is an Ingress resource functional without an Ingress Controller?

## 9. kubectl and YAML
108. What is kubectl?
109. How do you list Pods, Nodes, Deployments, and Services?
110. How do you inspect a resource with kubectl describe?
111. How do you fetch logs from a Pod?
112. How do you open a shell inside a container?
113. What does kubectl apply -f do?
114. What is the difference between kubectl apply and kubectl create?
115. How do you view the YAML definition of a running resource?
116. How do you change the current namespace for a command?
117. How do you delete a Kubernetes resource?
118. What are apiVersion, kind, metadata, and spec in a manifest?
119. What is declarative configuration?
120. What is the difference between imperative and declarative management?

## 10. Probes and Application Health
121. What is a liveness probe?
122. What is a readiness probe?
123. What is a startup probe?
124. What is the difference between liveness, readiness, and startup probes?
125. What happens when a liveness probe fails?
126. What happens when a readiness probe fails?
127. What probe types does Kubernetes support?
128. What do initialDelaySeconds, periodSeconds, timeoutSeconds, and failureThreshold mean?
129. How would you implement health endpoints for a Node.js application?
130. Why can a badly configured liveness probe cause production incidents?

## 11. Resource Requests, Limits, and QoS
131. What is a CPU request?
132. What is a CPU limit?
133. What is a memory request?
134. What is a memory limit?
135. What is the difference between requests and limits?
136. What is CPU throttling?
137. What does OOMKilled mean?
138. What are the Kubernetes QoS classes?
139. What is the difference between Guaranteed, Burstable, and BestEffort QoS?
140. How do resource requests affect Pod scheduling?
141. How do you investigate high CPU or memory usage in a Pod?

## 12. Scheduling and Node Management
142. What does the Kubernetes scheduler do?
143. What is nodeSelector?
144. What is node affinity?
145. What are Pod affinity and anti-affinity?
146. What are taints and tolerations?
147. What is the difference between node affinity and taints/tolerations?
148. How do you schedule a Pod onto a specific node?
149. What is a DaemonSet and when would you use it?
150. What happens to workloads when a worker node becomes NotReady?
151. What is a PodDisruptionBudget?
152. What is the difference between voluntary and involuntary disruptions?

## 13. Autoscaling
153. What is the Horizontal Pod Autoscaler (HPA)?
154. How does HPA scale workloads based on CPU or memory utilization?
155. What is the Metrics Server?
156. What is the difference between HPA and Vertical Pod Autoscaler (VPA)?
157. What is the Cluster Autoscaler?
158. What is the difference between Pod autoscaling and cluster autoscaling?
159. Why must resource requests be configured for CPU-utilization-based HPA?
160. How would you troubleshoot an HPA that does not scale?

## 14. Security and RBAC
161. What is Kubernetes RBAC?
162. What is a Role?
163. What is a ClusterRole?
164. What is a RoleBinding?
165. What is a ClusterRoleBinding?
166. What is the difference between Role and ClusterRole?
167. What is the difference between RoleBinding and ClusterRoleBinding?
168. What is a ServiceAccount?
169. How do you follow the principle of least privilege in Kubernetes?
170. How should Secrets and service account tokens be handled securely?
171. What are Pod Security Standards?
172. Why should containers avoid running as root?

## 15. Stateful Workloads, Jobs, and CronJobs
173. What is a StatefulSet?
174. What is the difference between a StatefulSet and a Deployment?
175. What is a headless Service and how is it used with StatefulSets?
176. What is a DaemonSet?
177. What is a Job?
178. What is a CronJob?
179. What is the difference between a Job and a CronJob?
180. How should you run database workloads on Kubernetes?
181. Why might a managed database be preferable to running MongoDB inside a cluster?
182. What should you consider when backing up persistent database storage?

## 16. Docker, Registry, and Image Management
183. How does Kubernetes run images built with Docker?
184. Does Kubernetes require Docker Engine as its container runtime?
185. What is imagePullPolicy?
186. How do you pull an image from a private container registry?
187. What is imagePullSecret?
188. How do you tag and publish an application image for Kubernetes?
189. Why should production images use reliable version tags instead of relying on latest?
190. How would you migrate a Docker Compose project to Kubernetes?

## 17. MERN Stack on Kubernetes
191. How would you deploy a MERN application to Kubernetes?
192. Why separate React frontend and Node.js backend into different Deployments?
193. How would the frontend reach the backend in a Kubernetes environment?
194. How would the backend connect to MongoDB through a stable endpoint?
195. Where would you store a MongoDB connection string?
196. How would you configure frontend and backend environment variables?
197. How would you expose the React frontend to external users?
198. How would you scale the Node.js backend to multiple replicas?
199. How would a Kubernetes Service distribute traffic across backend Pods?
200. How would you handle file uploads and shared files for multiple backend replicas?
201. How would you configure health checks for an Express API?
202. How would you deploy a new MERN version with minimal downtime?
203. How would you deploy a MERN app to Amazon EKS?
204. What is the relationship between Kubernetes, Nginx, and an AWS Load Balancer?
205. Draw and explain a production-ready MERN architecture on Kubernetes.

## 18. Troubleshooting and Scenario-Based Questions
206. A Pod is stuck in Pending. How would you investigate it?
207. A Pod is in CrashLoopBackOff. What steps would you take?
208. A Pod shows ImagePullBackOff. How would you troubleshoot it?
209. A Pod is Running, but the application is not responding. What would you check?
210. A Service cannot reach its backend Pods. How would you debug it?
211. A Service has no endpoints. What could be wrong?
212. An application is not accessible externally. How would you troubleshoot it?
213. A Deployment update causes errors. How would you roll back safely?
214. A Pod keeps getting OOMKilled. What would you investigate?
215. CPU usage suddenly increases across backend replicas. What would you do?
216. One worker node becomes unavailable. What happens to its workloads?
217. A ConfigMap value changed but the application still uses the old value. Why?
218. A PVC remains Pending. How would you find the cause?
219. DNS resolution between two Pods fails. What would you inspect?
220. HPA shows unknown metrics or does not scale. What would you check?
221. How would you perform a zero-downtime deployment?
222. How would you securely provide credentials to a production application?
223. How would you debug a MongoDB connection failure from a Node.js Pod?
224. How would you investigate a workload that works locally but fails in Kubernetes?
225. What would you check first during a production Kubernetes incident?

## Suggested Study Order

Start with questions 1–60 (fundamentals, architecture, Pods, and Deployments), then Services/networking, ConfigMaps/Secrets, storage, probes, and kubectl. After the core concepts, focus on troubleshooting and the MERN + AWS/EKS scenarios.

## Safety Note

Practise destructive commands only in a test cluster. Do not commit passwords, API keys, access tokens, production credentials, kubeconfig files, or real `.env` files.
