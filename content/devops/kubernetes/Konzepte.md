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
- *new ip address on re-creation*
- *every pod gets a unique IP and hostname and within a pod, containers can talk to each other via localhost*
- *containers in one pod can communicate via shared memory*
- *Under the hood, they heavily rely on Linux namespaces and cgroups*
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

### Service
- *permanent (static) ip address & DNS name that can be 'attached' to a pod*
- *lifecycle of service and pod are not connected*
- *load balancer; can be attached to multiple pods (on different nodes)*

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

### Volumes
- *for persistent data*
- *attaches physical storage to pod*
- *storage is on local node or remote (outside of k8s cluster)*

### Deployment
- *abstraction on top of pod*
- *blueprint for creating pods*
- *in practice, you don't create or work with pods directly*
- *checks on the health of your Pod and restarts the Pod's Container if it terminates. Deployments are the recommended way to manage the creation and scaling of Pods.*
- *DBs can't be replicated via Deployment (not stateless)*
- *manages replicasets*
- *everything below deployments is managed automatically by k8s*

### StatefulSet
- *meant for stateful applications like databases*
- *replicate stateful apps*
- *DBs are often hosted outside of the k8s cluster*
- [HN - Kubernetes StatefulSets are Broken, 13.8.22](https://news.ycombinator.com/item?id=32439255)

### Replicaset
- *manages the replicas of a pod*
- *in practice, you don't create, update or delete replicasets, you work with deployments*

### NetworkPolicy

### ResourceQuota
- *provides constraints that limit aggregate resource consumption per namespace. It can limit the quantity of objects that can be created in a namespace by type, as well as the total amount of compute resources that may be consumed by resources in that namespace.*
