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
- Probes
  - Startup
    - die anderen Probes werden nicht durchgeführt, bevor Startup erfolgt ist 
  - Readiness
    - prüft, ob der Pod Traffic entgegennehmen kann (z. B. wenn DB erreicht werden kann) 
  - Liveness
    - Failure führt zu Restart
  - mögliche Actions: Exec, TcpSocket, HttpGet
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
- *Pods in a StatefulSet are individually assigned their own Persistent Volume claims. The Pod’s volume will be reattached after it’s rescheduled, providing stable storage access after a rollout or scaling operation.*
- [HN - Kubernetes StatefulSets are Broken, 13.8.22](https://news.ycombinator.com/item?id=32439255)
- <https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/>

#### DaemonSet
- <https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/>

### Service
- *permanent (static) ip address & DNS name that can be 'attached' to a pod*
- *lifecycle of service and pod are not connected*
- *load balancer; can be attached to multiple pods (on different nodes)*
- *Each Service object defines a logical set of endpoints (usually these endpoints are Pods) along with a policy about how to make those pods accessible*
- Zuordnung zu Pods über Labels, ermöglicht Blue/Green-Deployments
- <u>Types</u>
  - ClusterIP
    - Default
    - Sichtbarkeit: im Cluster
    - `spec.ports.port` und `spec.ports.targetPort` (=Pod-Port)
    - *provides a load-balanced IP address*
    - *currently, depending on the proxy mode, for ClusterIP it's just round robin/random. It's done by kube-proxy, which runs on each nodes, proxies UDP and TCP and provides load balancing.*
    - *Choosing this value makes the Service only reachable from within the cluster*
    - *You can expose the service to the public with an Ingress or the Gateway API.*
  - NodePort
    - Erweiterung von ClusterIP
    - hat zusätzlich `spec.ports.nodePort` (Wert zw. 30.000 und 32.767), wo der Service von extern erreichbar ist
    - Sichtbarkeit: intern und extern (sofern die Node eine External IP hat)
    - *Exposes the Service on each Node's IP at a static port (the NodePort)* 
  - LoadBalancer
    - *Exposes the Service externally using a cloud provider's load balancer.*
    - Layer 4 (TCP); Simple Verfahren wie Round Robin möglich. Kein Message-Content-basiertes Load-Balancing möglich.
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
- Standardmäßig wird die Historie der letzten 3 erfolgreichen (`successfulJobsHistoryLimit`) und des letzten gescheiterten CronJobs aufbewahrt
- <https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/>

### Ingress
- *entry point for external requests*
- *forwards incoming requests to services*
- Layer 7 (Http, Smtp, ...); Komplexere LB-Verfahren möglich; z. B. auf Basis des Message-Contents, Path-Rewrites, ...
- <https://kubernetes.io/docs/concepts/services-networking/ingress/>

### ConfigMap
- *external configuration of application*
- *connected to pod*
- *usually contains URLs of database*
- *accessed via environment variables or properties file*
- Pod muss neu gestartet werden, um Änderungen zu sehen. ConfigMaps können aber auch als File gemounted werden, dann "live".
- <https://kubernetes.io/docs/concepts/configuration/configmap/>

### Secret
- *like ConfigMap, for secret data (credentials, certificates)*
- *stored in Base64*
- Sonderfall `Pod.spec.imagePullSecrets`

### Storage
- <https://medium.com/devops-mojo/kubernetes-storage-options-overview-persistent-volumes-pv-claims-pvc-and-storageclass-sc-k8s-storage-df71ca0fccc3>
  - *PV — low level representation of a storage volume. abstraction for the physical storage device that attached to the cluster. PV is not Namespaced, it is available to whole cluster. can be provisioned dynamically using Storage Classes, or they can be explicitly created by a cluster administrator.*
  - *PVC — binding between a Pod and Persistent Volume. PVC must be in same namespace as the Pod.*
  - *SC — allows for dynamic provisioning of Persistent Volumes. abstracts underlying storage provider. use provisioners that are specific to the storage platform or cloud provider to give Kubernetes access to the physical storage.*

#### Persistent Volume
- *for persistent data*
- *attaches physical storage to pod*
- *storage is on local node or remote (outside of k8s cluster)*
- *provisioned by administrator*
- Types
  - NFS
  - HostPath (nur für Development geeignet)
  - Flocker
  - diverse Cloud-spezifische
  - uvm.
- Reclaiming (`spec.persistentVolumeReclaimPolicy`)
  - *When a user is done with their volume, they can delete the PVC objects from the API that allows reclamation of the resource. The reclaim policy for a PersistentVolume tells the cluster what to do with the volume after it has been released of its claim.* 
  - Retain
    - *When the PersistentVolumeClaim is deleted, the PersistentVolume still exists and the volume is considered "released". But it is not yet available for another claim because the previous claimant's data remains on the volume. An administrator can manually reclaim the volume* 
  - Delete (Default)
    - *deletion removes both the PersistentVolume object from Kubernetes, as well as the associated storage asset in the external infrastructure* 
  - Recycle
    - deprecated 
  - <https://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming>
- Access Modes
  - ReadWriteMany - volume can be mounted as read-write by many nodes
  - ReadOnlyMany - volume can be mounted read-only by many nodes
  - ReadWriteOnce - volume can be mounted as read-write by a single node
  - ReadWriteOncePod - volume can be mounted as read-write by a single Pod
  - <https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes>

#### StorageClass
- *provides a way for administrators to describe the "classes" of storage they offer. Different classes might map to quality-of-service levels, or to backup policies, or to arbitrary policies determined by the cluster administrators.*
- Reclaim Policies
  - Retain
  - Delete (Default)
- `privisioner`: z. B. `kubernetes.io/azure-disk`
- <https://kubernetes.io/docs/concepts/storage/storage-classes/>

#### Persistent Volume Claim
- Das PVC kann ein Persistent Volume oder eine StorageClass referenzieren
- Ein PV kann nur ein einziges Mal geclaimed werden (Speicher ggf. verschwendet), eine StorageClass mehrmals

### NetworkPolicy
- By Default
  - können alle Container eines Pods miteinander 
  - alle Pods miteinander
  - alle Nodes mit allen Pods
  kommunizieren. Mit NetworkPolicies kann dies eingeschränkt werden. Z. B. intern nur Pods eines best. Namespaces, nach außen nur best. IP-Adressen erlaubt.
- *For Network Policies to take effect, <mark>your cluster needs to run a network plugin which also enforces them</mark>. Project Calico or Cilium are plugins that do so. This is not the default when creating a cluster!*
- <https://kubernetes.io/docs/concepts/services-networking/network-policies/>

### ResourceQuota
- *provides constraints that limit aggregate resource consumption per namespace. It can limit the quantity of objects that can be created in a namespace by type, as well as the total amount of compute resources that may be consumed by resources in that namespace.*

### Operator
- <https://kubernetes.io/docs/concepts/extend-kubernetes/operator/>

### Custom Resource Definitions (CRDs)
- <https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/>

### HorizontalPodAutoscaler
- automatisch Skalieren (Replicas) je nach Ressourcenverrbauch (CPU, RAM) oder benutzerdefinierte Metriken
- *... fragt der Controller Manager die Ressourcennutzung anhand der in jeder HorizontalPodAutoscaler Definition angegebenen Metriken ab. Der Controller Manager bezieht die Metriken entweder aus der Resource Metrics API (für Ressourcenmetriken pro Pod) oder aus der Custom Metrics API (für alle anderen Metriken).*
- <https://learnk8s.io/autoscaling-apps-kubernetes>
- <https://kubernetes.io/de/docs/tasks/run-application/horizontal-pod-autoscale/>

### VerticalPodAutoscaler


## Best Practice
- **Labels**
  - <https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/>
- **Config**
  - <https://kubernetes.io/docs/concepts/configuration/overview/> 
