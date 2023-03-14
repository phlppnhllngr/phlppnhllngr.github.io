---
title: Konzepte
parent: Kubernetes
grand_parent: DevOps
---

# Konzepte

## Komponenten, Terminologie

### Node
- *simple server, physical or virtual machine*
- **master node**
  - aka Control Plane 
  - *demand less resources than worker nodes*
  - *4 processes ("master components") run on every master node*
    - *API Server*
      - *cluster gateway*
      - *validates authentication*
      - *forwards requests: deploy new apps, create new services, schedule pods*
      - REST interface
      - alle Clients (inkl. kubectl) kommunizieren nur mit API Server
    - *Scheduler*
      - *schedule new pods*
      - *decides on which node (based on resource exhaustion) to put the new pod*
    - *Controller manager*
      - *detects and re-schedules (via request to Scheduler) crashed pods*
    - *etcd*
      - *key-value-store of cluster state (resources, health)*
      - *distributed among the cluster's master nodes*
      - *the cluster's "brain", single source of truth*
      - *does not contain application data*
      - nur der API Server kommuniziert mit etcd
  - Addons für
    - DNS
    - Web UI
    - Cluster-Level Logging
    - Monitoring  
- **worker node**
  - *multiple pods can run on one node (eg. application pod, database pod)*
  - *3 processes must be installed on every node*
    - *container runtime*
      - Containerd, Moby, Cri-o, ...
      - <mark>ab K8s v1.19 ist die Docker-Runtime nicht mehr enthalten</mark> => `crictl` statt `docker` auf den Nodes (SSH)
    - *kubelet*
      - *interacts with the container and the node*
      - *starts the pod with a container inside*
      - *assigns resources (CPU, RAM, storage) from node to the container*
    - *Kube proxy (k-proxy)*
      - *forwards requests from services to pods*

### Namespace
- Zwecks Gruppierung von Ressourcen
- z. B. Dev, Test, Prod
- Objekte eines Namespaces können auf welche in anderen zugreifen, sofern nicht via `NetworkPolicy` eingeschränkt
- `ResourceQuotas` beziehen sich auf einen NS
- Löschen eines NS bewirkt Löschen aller zugehörigen Ressourcen
- Pod.yaml: `metadata.namespace=<ns>`

### Pod
- *smallest unit of k8s*
- *abstraction over container*
- *usually one container per pod*
- *each pod gets own ip address*
- *new ip address on re-creation (ephemeral IP)*
- *every pod gets a unique IP and hostname and within a pod, containers can talk to each other via localhost*
- *containers in one pod can communicate via shared memory*
- *Under the hood, they heavily rely on Linux namespaces and cgroups*
- `spec.containers.*.command`: *corresponding to a Docker ENTRYPOINT*
- State
  - Pending
  - Running
    - Pod wurde einer Node zugewiesen 
  - Succeeded (exit code 0)
  - Failed (exit code != 0)
  - Unkown
  - CrashLoopBackoff
    - Gestartet -> Gecrashed -> Neu gestartet -> wieder gecrashed
- initContainers 
  ```yaml
  spec:
    initContainers:
      - name: wait-for-db
        image: busybox:1.28
        command: ['sh', '-c', "until nslookup my-db; do echo waiting for my-db; sleep 2; done"]
  ```
  - haben keine Probes
  - mehrere (sequentiall) möglich
- Zuordnung zu anderen Ressourcen
  - Pods können bei Bedarf best. Nodes zugeordnet werden
    - `spec.nodeSelector`: Key-Value-Paare (Labels der Node)
    - `spec.affinity.nodeAffinity`: komplexe Expressions
  - Pods können bei Bedarf anderen Pods zugeordnet werden (im Sinne von: laufen dann auf der gleichen Node)
    - `spec.affinity.podAffinity` bzw. auch `spec.affinity.podAntiAffinity`
- Use cases für mehrere Container pro Pod
  - Sidecar-Container, der Logfiles archiviert
  - Adapter, z. B. Format von Monitoring-Output umwandeln um für zentrales Monotoring-Tool aufzubereiten
- <https://kubernetes.io/docs/concepts/workloads/pods/>

### Workloads

#### ReplicaSet
- *manages the replicas of a pod*
- *provides self-healing capabilities (crashed Pods will be replaced automatically)*
- *in practice, you don't create, update or delete replicasets, you work with deployments*
- `spec.replicas=<number>`
- <https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/>

#### Deployment
- *abstraction on top of pod*
- *blueprint for creating pods*
- *in practice, you don't create or work with pods directly*
- *checks on the health of your Pod and restarts the Pod's Container if it terminates. Deployments are the recommended way to manage the creation and scaling of Pods.*
- *DBs can't be replicated via Deployment (not stateless)*
- *manages replicasets (in the background)*
- *everything below deployments is managed automatically by k8s*
- Mit Pods alleine nicht gegeben: Self-healing, Scaling, Updates, Rollback
- `spec.revisionHistoryLimit=<number>`
- `spec.strategy`
  - RollingUpdate
    - Pods werden nach und nach beendet und in neuer Version gestartet 
  - Recreate  
    - Erst werden alle Pods beendet, dann neue gestartet
- <https://kubernetes.io/docs/concepts/workloads/controllers/deployment/>

#### StatefulSet
- *replicate stateful applications like databases*
- *DBs are often hosted outside of the k8s cluster*
- *persistent volume claims (PVCs) are stable for StatefulSets, so if a pod dies and gets rescheduled in another node, the same volume is mounted in the new node with the same data.*
- Beim Runterskalieren oder Löschen werden PVC nicht automatisch entfernt
- Verwendung zusammen mit headless service
- [HN - Kubernetes StatefulSets are Broken, 13.8.22](https://news.ycombinator.com/item?id=32439255)
- <https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/>

#### DaemonSet
- <https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/>

### Service
- *permanent (static) ip address & DNS name that can be 'attached' to a pod*
- *lifecycle of service and pod are not connected*
- *load balancer; can be attached to multiple pods (on different nodes)*
- *Each Service object defines a logical set of endpoints (usually these endpoints are Pods) along with a policy about how to make those pods accessible*
- <u>Types</u>
  - ClusterIP
    - Default
    - *provides a load-balanced IP address*
    - *currently, depending on the proxy mode, for ClusterIP it's just round robin/random. It's done by kube-proxy, which runs on each nodes, proxies UDP and TCP and provides load balancing.*
    - *Choosing this value makes the Service only reachable from within the cluster*
    - *You can expose the service to the public with an Ingress or the Gateway API.*
  - NodePort
    - *Exposes the Service on each Node's IP at a static port (the NodePort)* 
  - LoadBalancer
    - *Exposes the Service externally using a cloud provider's load balancer.* 
  - ExternalName
    - *Maps the Service to the contents of the externalName field (e.g. foo.bar.example.com), by returning a CNAME record with its value*
- headless
  - <https://stackoverflow.com/a/52713482/7437541>
  - die Pods des zugeordneten Headless Services erreichen sich gegenseitig als \<podname>.\<servicename>
  - <https://kubernetes.io/docs/concepts/services-networking/service/#headless-services> 
- <https://kubernetes.io/docs/concepts/services-networking/service/>

### Endpoints
- *an Endpoints (the resource kind is plural) defines a list of network endpoints, typically referenced by a Service to define which Pods the traffic can be sent to.
The EndpointSlice API is the recommended replacement for Endpoints.*

### EndpointSlices
- *offer a more scalable and extensible alternative to Endpoints*
- <https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/>

#### Tasks

##### Job
- <https://kubernetes.io/docs/concepts/workloads/controllers/job/>

##### CronJob
- <https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/>

### Ingress
- *entry point for external requests*
- *forwards incoming requests to services*

### ConfigMap
- *external configuration of application*
- *connected to pod*
- *usually contains URLs of database*
- *accessed via environment variables or properties file*

### Secret
- *like ConfigMap, for secret data (credentials, certificates)*
- *stored in Base64*

### Persistent Volumes
- *for persistent data*
- *attaches physical storage to pod*
- *storage is on local node or remote (outside of k8s cluster)*

### Persistent Volume Claims

### NetworkPolicy
- By Default
  - können alle Container eines Pods miteinander 
  - alle Pods miteinander
  - alle Nodes mit allen Pods
  kommunizieren

### ResourceQuota
- *provides constraints that limit aggregate resource consumption per namespace. It can limit the quantity of objects that can be created in a namespace by type, as well as the total amount of compute resources that may be consumed by resources in that namespace.*

### Operator
- <https://kubernetes.io/docs/concepts/extend-kubernetes/operator/>

### Custom Resource Definitions (CRDs)
- <https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/>
