# Kubernetes Most Asked Interview Questions

A topic-wise Kubernetes interview preparation list in English, focused on Kubernetes fundamentals, architecture, MERN deployments, Docker, AWS/EKS, and scenario-based troubleshooting.

## Part 1 — Kubernetes Fundamentals

1. What is Kubernetes?
2. Why do we need Kubernetes?
3. What are the main benefits of Kubernetes?
4. What is the difference between Kubernetes and Docker?
5. What is a container?
6. What is the difference between Kubernetes and Docker Compose?
7. What is Kubernetes architecture?
8. What is a Kubernetes cluster?
9. What is a node?
10. What is a master node / control plane?
11. What is a worker node?
12. What is a Pod?
13. What is the difference between a container and a Pod?
14. What is a Namespace in Kubernetes?
15. What is a Deployment in Kubernetes?
16. What is a Service in Kubernetes?
17. What is a ReplicaSet in Kubernetes?
18. What is a ReplicationController in Kubernetes?
19. What is the difference between a Deployment and a ReplicaSet?
20. Why do we use a Deployment instead of deploying a Pod directly?

---

## Part 2 — Kubernetes Architecture

21. What are the components of the Kubernetes Control Plane?
22. What does `kube-apiserver` do?
23. What is `etcd`?
24. What does `kube-scheduler` do?
25. What does `kube-controller-manager` do?
26. What is `cloud-controller-manager`?
27. What are the components of a Worker Node?
28. What does `kubelet` do?
29. What does `kube-proxy` do?
30. What is a container runtime?
31. How is a request processed internally by Kubernetes?
32. What is the role of the API Server?
33. What data is stored in etcd?
34. How does the Scheduler assign a Pod to a Node?
35. What does the Controller Manager monitor?

---

## Part 3 — Pods

36. What is a Pod?
37. Why would you run multiple containers in one Pod?
38. What is a multi-container Pod?
39. What is a sidecar container?
40. What is the Pod lifecycle?
41. What are the different Pod states?
42. What do `Pending`, `Running`, `Succeeded`, `Failed`, and `Unknown` mean?
43. What is a Pod restart policy?
44. What is `CrashLoopBackOff`?
45. What is `ImagePullBackOff`?
46. How do you restart a Pod manually?
47. How do you check Pod logs?
48. How do you open a shell inside a Pod?
49. How do you check a Pod's IP address?
50. What happens after a Pod is deleted?

---

## Part 4 — Deployment and ReplicaSet

51. What is a Deployment?
52. How does a Deployment work?
53. What is the difference between a Deployment and a Pod?
54. What is the difference between a Deployment and a ReplicaSet?
55. How do you define the number of replicas?
56. How do you scale a Deployment?
57. What is a rolling update?
58. What is a rollback in Kubernetes?
59. How do you roll back a Deployment to its previous version?
60. What is `kubectl rollout`?
61. What is the difference between the `RollingUpdate` and `Recreate` strategies?
62. What does `replicas` mean in a Deployment?
63. What is a `selector` in a Deployment?
64. What role do labels play in a Deployment?
65. What happens if one Pod crashes?

---

## Part 5 — Services and Networking

66. What is a Kubernetes Service?
67. Why do we need a Service?
68. Why shouldn't we rely directly on Pod IP addresses?
69. What are the types of Kubernetes Services?
70. What is ClusterIP?
71. What is NodePort?
72. What is a LoadBalancer Service?
73. What is ExternalName?
74. What is the difference between ClusterIP and NodePort?
75. What is the difference between NodePort and LoadBalancer?
76. How does a Service identify Pods?
77. What is a Service selector?
78. What is Kubernetes DNS?
79. How does one Pod access another Pod?
80. How does an application continue working if a Service IP changes?

---

## Part 6 — ConfigMap and Secrets

81. What is a ConfigMap?
82. Why do we need a ConfigMap?
83. What is a Secret?
84. What is the difference between a ConfigMap and a Secret?
85. How do you provide environment variables in Kubernetes?
86. How do you inject a Secret into a Pod?
87. How do you mount a Secret as a file?
88. Are Kubernetes Secrets actually secure?
89. Does a Pod restart automatically when a ConfigMap is updated?
90. What can you use in Kubernetes as an alternative to a `.env` file?

---

## Part 7 — Volumes and Storage

91. What is a Kubernetes Volume?
92. How do you persist data used by a Pod?
93. What is `emptyDir`?
94. What is a PersistentVolume (PV)?
95. What is a PersistentVolumeClaim (PVC)?
96. What is the difference between a PV and a PVC?
97. What is a StorageClass?
98. What is dynamic provisioning?
99. How do you manage storage for a stateful application?
100. What happens to data when a Pod is deleted?

---

## Part 8 — Ingress

101. What is Kubernetes Ingress?
102. Why do we need Ingress?
103. What is the difference between Ingress and a Service?
104. What is an Ingress Controller?
105. What is the NGINX Ingress Controller?
106. How do you connect a domain to an application running in Kubernetes?
107. How do you configure HTTPS/SSL in Kubernetes?
108. What is path-based routing in Ingress?
109. What is host-based routing?
110. What is the difference between LoadBalancer and Ingress?

This section is especially important for your NGINX, MERN, and Kubernetes preparation.

---

## Part 9 — kubectl Commands

111. What is `kubectl`?
112. How do you list Pods?
113. How do you list Nodes?
114. How do you check Deployments?
115. How do you check Services?
116. How do you check Pod logs?
117. How do you enter a Pod?
118. How do you describe a Pod?
119. How do you scale a Deployment?
120. How do you restart a Deployment?
121. How do you roll back a Deployment?
122. How do you apply a YAML file?
123. How do you delete Kubernetes resources?
124. How do you check or change the current Namespace?
125. How do you view a Pod's YAML configuration?

---

## Part 10 — Health Checks

126. What is a Kubernetes liveness probe?
127. What is a readiness probe?
128. What is a startup probe?
129. What is the difference between liveness and readiness probes?
130. Why do we need a startup probe?
131. What happens if a liveness probe fails?
132. What happens if a readiness probe fails?
133. How do you configure an HTTP health check?
134. What is a TCP probe?
135. What is an exec probe?

---

## Part 11 — Resource Management

136. What is a CPU request?
137. What is a CPU limit?
138. What is a memory request?
139. What is a memory limit?
140. What is the difference between a request and a limit?
141. What problems can occur if you do not specify resources for a Pod?
142. What does `OOMKilled` mean?
143. What are Kubernetes QoS classes?
144. What is the difference between Guaranteed, Burstable, and BestEffort?
145. How does Kubernetes schedule a Pod on a Node?

---

## Part 12 — Scheduling

146. What does the Kubernetes Scheduler do?
147. What is a node selector?
148. What is node affinity?
149. What is Pod affinity?
150. What is Pod anti-affinity?
151. What are taints?
152. What are tolerations?
153. What is a real-world use case for taints and tolerations?
154. How do you run a Pod on a specific Node?
155. What role does resource availability play in Kubernetes scheduling?

---

## Part 13 — Autoscaling

156. What is HPA in Kubernetes?
157. What does the Horizontal Pod Autoscaler do?
158. How does HPA scale based on CPU usage?
159. What is the Vertical Pod Autoscaler?
160. What is the difference between HPA and VPA?
161. What is the Cluster Autoscaler?
162. What is the difference between HPA and the Cluster Autoscaler?
163. How do you implement automatic scaling in Kubernetes?

---

## Part 14 — Security

164. How does Kubernetes handle security?
165. What is RBAC?
166. What is a Role?
167. What is a ClusterRole?
168. What is a RoleBinding?
169. What is a ClusterRoleBinding?
170. What is a ServiceAccount?
171. What is the difference between a Role and a ClusterRole?
172. What is the difference between a RoleBinding and a ClusterRoleBinding?
173. How do you grant a Pod only the minimum permissions it needs?
174. How do you secure Kubernetes Secrets?

---

## Part 15 — StatefulSet, DaemonSet, and Jobs

175. What is a StatefulSet?
176. What is the difference between a StatefulSet and a Deployment?
177. Why do Stateful applications use StatefulSets?
178. What is a DaemonSet?
179. What is a real-world use case for a DaemonSet?
180. What is a Job?
181. What is a CronJob?
182. What is the difference between a Job and a CronJob?
183. What does stable network identity mean in a StatefulSet?
184. What Kubernetes resource would you use to deploy a database?

---

## Part 16 — MERN and Kubernetes: Real-World Questions

These questions are especially important for a MERN developer because interviewers may ask how Kubernetes is used in practical application deployments.

185. How would you deploy a MERN application on Kubernetes?
186. How would you deploy a React frontend on Kubernetes?
187. How would you deploy a Node.js/Express backend on Kubernetes?
188. How would you deploy MongoDB in Kubernetes?
189. How many Pods would you use for a MERN application?
190. Why would you create separate Deployments for the frontend and backend?
191. How would the frontend communicate with the backend in Kubernetes?
192. How would the backend connect to MongoDB?
193. How would you store a MongoDB connection string in Kubernetes?
194. How would you configure environment variables in Kubernetes?
195. Where would you use ConfigMaps and Secrets in a MERN application?
196. How would you configure a readiness probe for a Node.js application?
197. How would you configure a liveness probe for a Node.js application?
198. How would you run multiple replicas of a backend?
199. How would traffic be distributed among multiple Node.js Pods?
200. How would you design the architecture for React, Node.js, and MongoDB on Kubernetes?

---

## Part 17 — Docker and Kubernetes

201. What is the relationship between Docker and Kubernetes?
202. How does Kubernetes use a Docker image?
203. What is the relationship between a Dockerfile and Kubernetes?
204. How do you deploy a Docker image in Kubernetes?
205. How does Kubernetes pull an image from Docker Hub?
206. How do you use an image from a private Docker registry in Kubernetes?
207. What is `imagePullPolicy`?
208. How does Kubernetes restart a container?
209. How would you migrate a Docker Compose application to Kubernetes?
210. What is the difference between Docker Compose and Kubernetes?

---

## Part 18 — Scenario-Based Questions

211. A Pod is in `CrashLoopBackOff`. How would you debug it?
212. A Pod is in the `Pending` state. What would you check?
213. A Pod shows `ImagePullBackOff`. What would you check?
214. A Service cannot access its Pods. How would you troubleshoot it?
215. An application is not accessible externally. What would you check?
216. The application goes down after a Deployment update. What would you do?
217. How would you find the reason a Kubernetes Pod keeps restarting?
218. An application's CPU usage suddenly reaches 90%. What would you do?
219. Memory usage keeps increasing. What would you investigate in Kubernetes?
220. What happens to a Node's Pods if that Node goes down?
221. How would you achieve zero-downtime deployment in Kubernetes?
222. An application has three replicas and one Pod fails. What happens?
223. How is application traffic distributed in Kubernetes?
224. What configuration would you use when deploying a Node.js application to production?
225. How would you secure an application running in a Kubernetes cluster?

---

## Priority Checklist for Amit

If you are preparing for interviews as a MERN developer with 3–4 years of experience, master these topics first.

### Must-Know Topics

1. What is Kubernetes?
2. Docker vs. Kubernetes
3. Kubernetes architecture
4. Pods
5. Deployments
6. ReplicaSets
7. Services
8. ClusterIP, NodePort, and LoadBalancer
9. ConfigMaps
10. Secrets
11. Ingress
12. Liveness and readiness probes
13. Resource requests and limits
14. HPA
15. Namespaces
16. PV and PVC
17. StatefulSets
18. RBAC
19. `kubectl` commands
20. Deploying a MERN application on Kubernetes
21. Debugging `CrashLoopBackOff`
22. Zero-downtime deployment
23. Docker and Kubernetes
24. Kubernetes with AWS/EKS
