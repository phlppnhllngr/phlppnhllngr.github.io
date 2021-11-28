---
tags: [Notebooks/DevOps]
title: Kubernetes
created: '2020-03-11T21:13:07.906Z'
modified: '2021-09-05T11:46:48.822Z'
parent: DevOps
---

# Kubernetes
- <https://kubernetes.io>
- *also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications*
- <https://dev.to/sandrogiacom/kubernetes-for-java-developers-setup-41nk> (minikube, kubectl, virtualbox)


## Komponenten, Terminologie
- **Pod**
  - *smallest unit of k8s*
  - *abstraction over container*
  - *usually one container per pod*
  - *each pod gets own ip address*
  - *new ip address on re-creation*
- **Service**
  - *permanent (static) ip address & DNS name that can be 'attached' to a pod*
  - *lifecycle of service and pod are not connected*
  - *load balancer; can be attached to multiple pods (on different nodes)*
- **Node**
  - *simple server, physical or virtual machine*
  - *worker node*
    - *multiple pods can run on one node (eg. application pod, database pod)*
    - *3 processes must be installed on every node*
      - *container runtime*
      - *kubelet*
        - *interacts with the container and the node*
        - *starts the pod with a container inside*
        - *assigns resources (CPU, RAM, storage) from node to the container*
      - *Kube proxy (k-proxy)*
        - *forwards requests from services to pods*
  - *master node*
    - *demand less resources than worker nodes*
    - *4 processes run on every master node*
      - *API Server*
        - *cluster gateway*
        - *validates authentication*
        - *forwards requests: deploy new apps, create new services, schedule pods*
      - *Scheduler*
        - *schedule new pods*
        - *decides on which node (based on resource exhaustion) to put the pod*
      - *Controller manager*
        - *detects and re-schedules (via request to Scheduler) crashed pods*
      - *etcd*
        - *key-value-store of cluster state (resources, health)*
        - *distributed among the cluster's master nodes*
        - *the cluster's "brain"*
        - *does not contain application data*
- **Ingress**
  - *entry point for external requests*
  - *forwards incoming requests to services*
- **ConfigMap**
  - *external configuration of application*
  - *connected to pod*
  - *usually contains URLs of database*
  - *accessed via environment variables or properties file*
- **Secret**
  - *like ConfigMap, for secret data (credentials, certificates)*
  - *stored in Base64*
- **Volumes**
  - *for persistent data*
  - *attaches physical storage to pod*
  - *storage is on local node or remote (outside of k8s cluster)*
- **Deployment**
  - *abstraction on top of pod*
  - *blueprint for creating pods*
  - *in practice, you don't create or work with pods directly*
  - *DBs can't be replicated via Deployment (not stateless)*
  - *manages replicasets*
  - *everything below deployments is managed automatically by k8s*
- **StatefulSet**
  - *meant for stateful applications like databases*
  - *replicate stateful apps*
  - *DBs are often hosted outside of the k8s cluster*
- **Replicaset**
  - *manages the replicas of a pod*
  - *in practice, you don't create, update or delete replicasets, you work with deployments*


## YAML-Konfigurationsdateien
- Bsp.:
  ```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: nginx
    labels:
      app: nginx
  spec: #specification for deployment
    replicas: 1
    selector:
      matchLabels:
        app: nginx
    template:
      metadata:
        labels:
          app: nginx
      spec: #specification for pods
        containers:
        - name: nginx
          image: nginx:1.16
          ports:
          - containerPort: 80
  ```

## Tools
- docker-desktop → Docker/Tools
- <https://yankee.dev/6-tools-to-run-kubernetes-locally>
- **kubectl**
  - *The kubectl command line tool lets you control Kubernetes clusters*
  - *submits commands to master-node's api server*
  - Commands
    - get
      - `kubectl get nodes|pod|services|deployment|replicaset`
    - create
      - `kubectl create -h`
      - deployment
        - *create and run pod and replicaset*
        - `kubectl create deployment <name> --image=<image> [--dry-run] [options]`
        - `kubectl create deployment nginx --image=nginx:latest`
    - edit
      - *edit deployment configurations*
      - `kubectl edit deployment nginx`
    - logs
      - `kubectl logs <pod>`
    - describe
      - `kubectl describe pod <pod>`
    - exec
      - `kubectl exec -it <pod> -- /bin/bash`
    - delete
      - `kubectl delete deployment <deployment>`
      - `kubectl delete -f <config-file>`
    - apply
      - *create or update a component (e. g. deployment) from config file*
      - *k8s knows whether to update or create the component*
      - `kubectl apply -f <config-file>`
  - <https://kubernetes.io/docs/reference/kubectl/>
- **minikube**
  - *Run Kubernetes locally*
  - *Minikube is the officially supported way to run Kubernetes locally on macOS, Windows, or Linux. Furthermore, it is the only tool that is a drop-in replacement for Docker Desktop.* (<https://matt-rickard.com/docker-desktop-alternatives/>)
  - *test local cluster setup where master processes and worker processes run on one node*
  - *node runs in virtual box*
  - *installs kubectl and docker runtime*
  - CLI commands
    - start
      - `minikube start --vm-driver=<driver> [--alsologtostderr]`
    - stop
    - status
      - Status von Host, kubelet, api server einsehen
    - dashboard
  - *minikube is for starting and deleting the cluster, for everything else use kubectl*
  - Drivers: Docker, VirtualBox, Podman, ... (<https://minikube.sigs.k8s.io/docs/drivers/>)
  - <https://github.com/kubernetes/minikube>
  - <https://minikube.sigs.k8s.io/docs/>
  - <https://kubernetes.io/docs/tutorials/hello-minikube/>
- **Helm**
  - <https://helm.sh>
  - *The package manager for Kubernetes*
  - *Helm is the best way to find, share, and use software built for Kubernetes.*
  - *Helm Charts help you define, install, and upgrade even the most complex Kubernetes application*
- **lens**
  - *The Kubernetes IDE*
  - <https://github.com/lensapp/lens>
- **kompose**
  - *go from Docker Compose to Kubernetes*
  - *takes a Docker Compose file and translates it into Kubernetes resources*
  - <https://github.com/kubernetes/kompose>
- **argo-cd**
  - *Declarative continuous deployment for Kubernetes.*
  - <https://github.com/argoproj/argo-cd> *6.8k
- **pixie**
  - *Instant Kubernetes-Native Application Observability*
  - *Use Pixie to view the high-level state of your cluster (service maps, cluster resources, application traffic) and also drill-down into more detailed views (pod state, flame graphs, individual full-body application requests).*
  - <https://github.com/pixie-io/pixie>
- **kubesphere**
  - *is a distributed operating system for cloud-native application management, using Kubernetes as its kernel*
  - *It provides developer-friendly wizard web UI*
  - <https://github.com/kubesphere/kubesphere>
- **kubeapps**
  - *web-based UI for deploying and managing applications in Kubernetes clusters*
  - <https://github.com/kubeapps/kubeapps>
