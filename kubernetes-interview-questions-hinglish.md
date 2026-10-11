# Kubernetes Most Asked Interview Questions

Topic-wise Kubernetes interview preparation questions in Hinglish, focused on fundamentals, architecture, MERN, Docker, AWS/EKS, and scenario-based interview preparation.

## Part 1 — Kubernetes Fundamentals

1. Kubernetes kya hai?
2. Kubernetes ki need kyu padti hai?
3. Kubernetes ke main benefits kya hain?
4. Kubernetes aur Docker mein kya difference hai?
5. Container kya hota hai?
6. Kubernetes aur Docker Compose mein kya difference hai?
7. Kubernetes architecture kya hai?
8. Kubernetes Cluster kya hota hai?
9. Node kya hota hai?
10. Master Node / Control Plane kya hota hai?
11. Worker Node kya hota hai?
12. Pod kya hota hai?
13. Container aur Pod mein kya difference hai?
14. Kubernetes mein Namespace kya hota hai?
15. Kubernetes mein Deployment kya hota hai?
16. Kubernetes mein Service kya hoti hai?
17. Kubernetes mein ReplicaSet kya hota hai?
18. Kubernetes mein ReplicationController kya hota hai?
19. Deployment aur ReplicaSet mein kya difference hai?
20. Pod ko directly deploy karne ke bajay Deployment kyu use karte hain?

## Part 2 — Kubernetes Architecture

21. Kubernetes Control Plane ke components kaunse hain?
22. `kube-apiserver` kya karta hai?
23. `etcd` kya hota hai?
24. `kube-scheduler` kya karta hai?
25. `kube-controller-manager` kya karta hai?
26. `cloud-controller-manager` kya hota hai?
27. Worker Node ke components kaunse hain?
28. `kubelet` kya karta hai?
29. `kube-proxy` kya karta hai?
30. Container Runtime kya hota hai?
31. Kubernetes request internally kaise process hoti hai?
32. API Server ka role kya hai?
33. etcd mein kya store hota hai?
34. Scheduler Pod ko Node kaise assign karta hai?
35. Controller Manager kya monitor karta hai?

## Part 3 — Pods

36. Pod kya hai?
37. Ek Pod mein multiple containers kyu rakhte hain?
38. Multi-container Pod kya hota hai?
39. Sidecar container kya hota hai?
40. Pod lifecycle kya hai?
41. Pod ke different states kaunse hain?
42. `Pending`, `Running`, `Succeeded`, `Failed`, `Unknown` ka kya meaning hai?
43. Pod restart policy kya hoti hai?
44. Pod CrashLoopBackOff kya hota hai?
45. ImagePullBackOff kya hota hai?
46. Pod ko manually restart kaise karenge?
47. Pod logs kaise check karenge?
48. Pod ke andar shell kaise open karenge?
49. Pod ka IP kaise check karenge?
50. Pod delete hone ke baad kya hota hai?

## Part 4 — Deployment & ReplicaSet

51. Deployment kya hai?
52. Deployment kaise kaam karta hai?
53. Deployment aur Pod mein difference?
54. Deployment aur ReplicaSet mein difference?
55. Replica count kaise define karte hain?
56. Deployment ko scale kaise karenge?
57. Rolling Update kya hota hai?
58. Kubernetes mein Rollback kya hota hai?
59. Deployment ka previous version kaise rollback karenge?
60. `kubectl rollout` kya hota hai?
61. `RollingUpdate` vs `Recreate` strategy?
62. Deployment mein `replicas` kya hota hai?
63. Deployment mein `selector` kya hota hai?
64. Deployment mein labels ka kya role hai?
65. Agar ek Pod crash ho jaye to Kubernetes kya karega?

## Part 5 — Services & Networking

66. Kubernetes Service kya hoti hai?
67. Service ki need kyu hoti hai?
68. Pod IP directly use kyu nahi karte?
69. Kubernetes Service ke types kaunse hain?
70. ClusterIP kya hai?
71. NodePort kya hai?
72. LoadBalancer Service kya hai?
73. ExternalName kya hai?
74. ClusterIP vs NodePort?
75. NodePort vs LoadBalancer?
76. Service Pod ko kaise identify karti hai?
77. Service selector kya hota hai?
78. Kubernetes DNS kya hota hai?
79. Ek Pod doosre Pod ko kaise access karta hai?
80. Service ka IP change hone par application kaise work karti hai?

## Part 6 — ConfigMap & Secrets

81. ConfigMap kya hota hai?
82. ConfigMap ki need kyu hoti hai?
83. Secret kya hota hai?
84. ConfigMap vs Secret?
85. Environment variables Kubernetes mein kaise provide karte hain?
86. Secret ko Pod mein kaise inject karte hain?
87. Secret ko file ke form mein kaise mount karte hain?
88. Kubernetes Secret actually secure hota hai kya?
89. ConfigMap update hone ke baad Pod automatically restart hota hai kya?
90. `.env` file ke alternative ke roop mein Kubernetes mein kya use karenge?

## Part 7 — Volumes & Storage

91. Kubernetes Volume kya hai?
92. Pod ke andar data persist kaise karenge?
93. EmptyDir kya hota hai?
94. PersistentVolume (PV) kya hai?
95. PersistentVolumeClaim (PVC) kya hai?
96. PV aur PVC mein difference?
97. StorageClass kya hota hai?
98. Dynamic Provisioning kya hoti hai?
99. Stateful application ke liye storage kaise manage karenge?
100. Pod delete hone ke baad data ka kya hota hai?

## Part 8 — Ingress

101. Kubernetes Ingress kya hai?
102. Ingress ki need kyu hoti hai?
103. Ingress vs Service?
104. Ingress Controller kya hota hai?
105. NGINX Ingress Controller kya hai?
106. Domain ko Kubernetes application se kaise connect karenge?
107. HTTPS/SSL Kubernetes mein kaise configure karenge?
108. Ingress mein path-based routing kya hoti hai?
109. Host-based routing kya hoti hai?
110. LoadBalancer vs Ingress?

**Note:** Nginx + MERN + Kubernetes preparation ke liye ye section especially important hai.

## Part 9 — kubectl Commands

111. `kubectl` kya hai?
112. Pods kaise list karenge?
113. Nodes kaise list karenge?
114. Deployments kaise check karenge?
115. Services kaise check karenge?
116. Pod ke logs kaise check karenge?
117. Pod ke andar kaise enter karenge?
118. Pod describe kaise karenge?
119. Deployment scale kaise karenge?
120. Deployment restart kaise karenge?
121. Deployment rollback kaise karenge?
122. YAML apply kaise karenge?
123. Kubernetes resources delete kaise karenge?
124. Current namespace kaise check/change karenge?
125. Kisi Pod ka YAML kaise dekhoge?

## Part 10 — Health Checks

126. Kubernetes Liveness Probe kya hai?
127. Readiness Probe kya hai?
128. Startup Probe kya hai?
129. Liveness vs Readiness Probe?
130. Startup Probe ki need kyu hoti hai?
131. Agar Liveness Probe fail ho jaye to kya hota hai?
132. Agar Readiness Probe fail ho jaye to kya hota hai?
133. HTTP health check kaise configure karenge?
134. TCP Probe kya hota hai?
135. Exec Probe kya hota hai?

## Part 11 — Resource Management

136. CPU Request kya hota hai?
137. CPU Limit kya hota hai?
138. Memory Request kya hota hai?
139. Memory Limit kya hota hai?
140. Request vs Limit?
141. Pod ko resources na dene par kya problem ho sakti hai?
142. OOMKilled kya hota hai?
143. QoS Classes kya hain?
144. Guaranteed vs Burstable vs BestEffort?
145. Kubernetes Pod ko Node par kaise schedule karta hai?

## Part 12 — Scheduling

146. Kubernetes Scheduler kya karta hai?
147. Node Selector kya hai?
148. Node Affinity kya hai?
149. Pod Affinity kya hai?
150. Pod Anti-Affinity kya hai?
151. Taints kya hain?
152. Tolerations kya hain?
153. Taints & Tolerations ka real-world use?
154. Pod ko specific Node par kaise run karenge?
155. Kubernetes scheduling mein resource availability ka kya role hai?

## Part 13 — Autoscaling

156. Kubernetes HPA kya hai?
157. Horizontal Pod Autoscaler kya karta hai?
158. HPA CPU usage ke basis par kaise scale karta hai?
159. Vertical Pod Autoscaler kya hai?
160. HPA vs VPA?
161. Cluster Autoscaler kya hai?
162. HPA vs Cluster Autoscaler?
163. Kubernetes mein automatic scaling kaise implement karenge?

## Part 14 — Security

164. Kubernetes security kaise handle karta hai?
165. RBAC kya hai?
166. Role kya hota hai?
167. ClusterRole kya hota hai?
168. RoleBinding kya hota hai?
169. ClusterRoleBinding kya hota hai?
170. ServiceAccount kya hai?
171. Role vs ClusterRole?
172. RoleBinding vs ClusterRoleBinding?
173. Pod ko minimum permissions kaise denge?
174. Kubernetes Secrets ko secure kaise karenge?

## Part 15 — StatefulSet / DaemonSet / Jobs

175. StatefulSet kya hota hai?
176. StatefulSet vs Deployment?
177. Stateful applications ke liye StatefulSet kyu use hota hai?
178. DaemonSet kya hota hai?
179. DaemonSet ka real-world use?
180. Job kya hota hai?
181. CronJob kya hota hai?
182. Job vs CronJob?
183. StatefulSet mein stable network identity kya hoti hai?
184. Kubernetes mein database deploy karne ke liye kya use karenge?

## Part 16 — MERN + Kubernetes Real-World Questions

Ye questions MERN developer interviews ke practical scenarios ke liye important hain.

185. MERN application ko Kubernetes par kaise deploy karoge?
186. React frontend ko Kubernetes par kaise deploy karoge?
187. Node.js/Express backend ko Kubernetes par kaise deploy karoge?
188. MongoDB ko Kubernetes mein kaise deploy karoge?
189. MERN application ke liye kitne Pods honge?
190. Frontend aur Backend ko separate Deployment kyu karenge?
191. Frontend backend ko Kubernetes mein kaise communicate karega?
192. Backend MongoDB ko kaise connect karega?
193. MongoDB connection string ko Kubernetes mein kaise store karoge?
194. Environment variables Kubernetes mein kaise configure karoge?
195. MERN application mein ConfigMap aur Secret kaha use karoge?
196. Node.js application ke liye Readiness Probe kaise banaoge?
197. Node.js application ke liye Liveness Probe kaise banaoge?
198. Backend ko multiple replicas mein kaise run karoge?
199. Multiple Node.js Pods ke beech traffic kaise distribute hoga?
200. Kubernetes mein React + Node + MongoDB ka architecture kaise design karoge?

## Part 17 — Docker + Kubernetes

201. Docker aur Kubernetes ka relationship kya hai?
202. Kubernetes Docker image ko kaise use karta hai?
203. Dockerfile ka Kubernetes se kya relation hai?
204. Docker image ko Kubernetes mein kaise deploy karte hain?
205. Docker Hub se image Kubernetes mein kaise pull hoti hai?
206. Private Docker registry ki image Kubernetes mein kaise use karenge?
207. `imagePullPolicy` kya hai?
208. Kubernetes mein container restart kaise hota hai?
209. Docker Compose application ko Kubernetes mein kaise migrate karoge?
210. Docker Compose vs Kubernetes?

## Part 18 — Scenario-Based Questions

211. Pod `CrashLoopBackOff` mein hai, debugging kaise karoge?
212. Pod `Pending` state mein hai, kya check karoge?
213. Pod `ImagePullBackOff` de raha hai, kya check karoge?
214. Service Pod ko access nahi kar pa rahi, debugging kaise karoge?
215. Application externally accessible nahi hai, kya check karoge?
216. Deployment update ke baad application down ho gayi, kya karoge?
217. Kubernetes Pod baar-baar restart ho raha hai, reason kaise find karoge?
218. Application ka CPU suddenly 90% ho gaya, kya karoge?
219. Memory continuously increase ho rahi hai, Kubernetes mein kya check karoge?
220. Ek Node down ho gaya, uske Pods ka kya hoga?
221. Kubernetes mein zero-downtime deployment kaise karoge?
222. Application ke 3 replicas hain, ek Pod fail ho gaya—kya hoga?
223. Kubernetes mein application ka traffic kaise distribute hota hai?
224. Production mein Node.js application deploy karte waqt kya configuration rakhoge?
225. Kubernetes cluster mein application ko secure kaise karoge?

## Priority — Must-Know Topics

Agar aap MERN Developer (3–4 years experience) ke interview ke liye prepare kar rahe hain, to pehle ye topics strong karein:

1. Kubernetes kya hai
2. Docker vs Kubernetes
3. Kubernetes Architecture
4. Pod
5. Deployment
6. ReplicaSet
7. Service
8. ClusterIP / NodePort / LoadBalancer
9. ConfigMap
10. Secret
11. Ingress
12. Liveness / Readiness Probe
13. Resource Request / Limit
14. HPA
15. Namespace
16. PV / PVC
17. StatefulSet
18. RBAC
19. `kubectl` commands
20. MERN application Kubernetes par deploy karna
21. CrashLoopBackOff debugging
22. Zero-downtime deployment
23. Docker + Kubernetes
24. Kubernetes + AWS/EKS
