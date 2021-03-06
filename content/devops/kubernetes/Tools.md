---
title: Tools
parent: Kubernetes
grand_parent: DevOps
---

# Tools
- docker-desktop → Docker/Tools
- <https://yankee.dev/6-tools-to-run-kubernetes-locally>
- **kubectl**
  - *The kubectl command line tool lets you control Kubernetes clusters. deploy applications, inspect and manage cluster resources, and view logs*
  - *submits commands to master-node's api server*
  - Commands
    - apply
      - *create or update a component (e. g. deployment) from config file*
      - *k8s knows whether to update or create the component*
      - `kubectl apply -f <config-file>`
    - config
      - view
        - `kubectl config view`
    - create
      - `kubectl create -h`
      - deployment
        - *create and run pod and replicaset*
        - `kubectl create deployment <name> --image=<image> [--dry-run] [options]`
        - `kubectl create deployment nginx --image=nginx:latest`
    - delete
      - `kubectl delete deployment <deployment>`
      - `kubectl delete -f <config-file>`
    - describe
      - `kubectl describe pod <pod>`
    - edit
      - *edit deployment configurations*
      - `kubectl edit deployment nginx`
    - exec
      - `kubectl exec -it <pod> -- /bin/bash`
    - expose
      - `kubectl expose deployment hello-node --type=LoadBalancer --port=8080`
      - *The --type=LoadBalancer flag indicates that you want to expose your Service outside of the cluster.*
      - *On cloud providers that support load balancers, an external IP address would be provisioned to access the Service. On minikube, the LoadBalancer type makes the Service accessible through the `minikube service` command.*
    - get
      - `kubectl get nodes|pod|services|deployment|replicaset|events`
    - logs
      - `kubectl logs <pod>`
  - <https://kubernetes.io/docs/reference/kubectl/>
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
- **kubespray**
  - *Deploy a Production Ready Kubernetes Cluster*
  - <https://github.com/kubernetes-sigs/kubespray>
- **telepresence**
  - *Local development against a remote Kubernetes or OpenShift cluster*
  - <https://github.com/telepresenceio/telepresence>
- **mizu**
  - *API traffic viewer for Kubernetes enabling you to view all API communication between microservices. Think TCPDump and Wireshark re-invented for Kubernetes*
  - <https://github.com/up9inc/mizu>
- **kustomize**
  - *introduces a template-free way to customize application configuration that simplifies the use of off-the-shelf applications. Now, built into kubectl as `apply -k`.*
  - <https://kustomize.io/>
- **kubernetes-client/java**
  - <https://github.com/kubernetes-client/java>