---
tags: [Notebooks/DevOps]
title: Kubernetes
created: '2020-03-11T21:13:07.906Z'
modified: '2021-09-05T11:46:48.822Z'
parent: DevOps
has_children: true
---

# Kubernetes
- Container Orchestration Engine
- <https://kubernetes.io>
- *also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications*
- <https://dev.to/sandrogiacom/kubernetes-for-java-developers-setup-41nk> (minikube, kubectl, virtualbox)
- <https://github.com/jayendrapatil/kubernetes-exercises>
- <https://flant.com/k8s-iceberg.svg>
- <https://github.com/kelseyhightower/kubernetes-the-hard-way> - *Bootstrap Kubernetes the hard way on Google Cloud Platform. No scripts.*
- <https://github.com/bregman-arie/devops-resources/blob/master/resources/kubernetes.md>
- <https://github.com/bregman-arie/devops-exercises/blob/master/topics/kubernetes/README.md>
- <https://github.com/techiescamp/kubernetes-learning-path> - *A roadmap to learn Kubernetes from scratch (Beginner to Advanced level)*
- <https://github.com/stefanprodan/podinfo> - *a tiny web application made with Go that showcases best practices of running microservices in Kubernetes.*
- [YT: Docker Containers and Kubernetes Fundamentals – Full Hands-On Course, 6h, 10/2022](https://www.youtube.com/watch?v=kTp5xUtcalw)


## Context
- besteht aus Cluster, einem User, einem namespace
- der aktuelle Context ist der Default für kubectl-Commands
- `kubectl config current-context` um den aktuellen Context zu erfahren


## kubectl
- *The kubectl command line tool lets you control Kubernetes clusters. deploy applications, inspect and manage cluster resources, and view logs*
- *submits commands to master-node's api server*
- Die Commands, die Ressourcen (Deployments, Pods, ...) betreffen, können z. T. auch via YAML-Files abgebildet werden (imperativ vs. deklarativ)
- Connection-Info gespeichert in $HOME/.kube/config
- <https://kubernetes.io/docs/reference/kubectl/cheatsheet/>
- <u>Commands</u>
  - **apply**
    - *create or update a component (e. g. deployment) from config file [declaratively]*
    - *k8s knows whether to update or create the component*
    - `kubectl apply -f <config-file>`
    - `--kustomize`
      - `kubectl apply -k path/to/kustomization.yaml`
      - für "Base"- und "Overlay"-Konfigurationen (z. B. Dev, Test, Prod)
      - `namespace=<ns>` um sicherzustellen, dass eine spezielle Konfig auch wirklich nur in der Vorgesehenen Umgebung (NS) applied wird
      - <https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/>
      - <https://kubectl.docs.kubernetes.io/references/kustomize/>
  - **cluster-info**
  - **config**
    - current-context
    - get-contexts
    - set-context
      - Namespace ändern: `set-context --current --namespace=<ns>`
    - use-context \<contextName>
    - view
      - `kubectl config view`
  - **create**
    - `kubectl create -h`
    - mit `--dry-run=client --output yaml --save-config > foo.yaml` können Ressourcen-Yamls erstellt werden
    - deployment
      - *create and run pod and replicaset*
      - `kubectl create deployment <name> --image=<image> [--dry-run] [--port] [--replicas=<number>] [...]`
  - **delete**
    - `kubectl delete deployment <deployment>`
    - `kubectl delete -f <config-file>`
    - `kubectl delete pod --grace-period=<number>`
    - `kubectl delete pod --grace-period=0 --force`
  - **describe**
    - `kubectl describe pod <pod>`
  - **edit**
    - *edit deployment configurations*
    - `kubectl edit deployment nginx`
  - **exec**
    - `kubectl exec -it <pod> -- /bin/sh`
  - **expose**
    - Erzeugt einen Service, um einen Pod oder ein Deployment zu exposen
    - `kubectl expose deploy --name=<name> --port=<number> --targetPort=<number>`
    - `kubectl expose deployment hello-node --type=LoadBalancer --port=8080`
    - *The --type=LoadBalancer flag indicates that you want to expose your Service outside of the cluster.*
    - *On cloud providers that support load balancers, an external IP address would be provisioned to access the Service. On minikube, the LoadBalancer type makes the Service accessible through the `minikube service` command.*
  - **get**
    - `kubectl get all|nodes|ns|pods|services|deployments|replicasets|events|endpoints|...`
    - `get pods --all-namespaces --output wide --selector=foo=bar`
    - `get pods -n <ns> | get pods --namespace=<ns>`
    - `get pod <podname> -o wide`
    - `get pod <podname> -o yaml > pod.yaml`
  - **kustomize**
    - gibt den von kustomize generierten Inhalt aus (Dry-Run)  
  - **logs**
    - `kubectl logs [--previous] <pod>`
  - **port-forward**
    - *in Kubernetes, every pod gets its own ip address from 10.*, that is usable only within the cluster. Now, the port-forward feature of kubectl simply tunnels the traffic from a specified port at your local host machine to the specified port on the specified pod. API server then becomes, in a sense, a temporary gateway between your local port and the Kubernetes cluster*
    - *kubectl port-forward is more generic as it can forward TCP traffic while kubectl proxy can only forward HTTP traffic.*
    - *useful for testing/debugging purposes so you can access your service locally without exposing it*
    - `kubectl port-forward pods/podname 8080:80`
    - `kubectl port-forward services/fooservice 8080:80`
  - **proxy**
  - **rollout**
    - für Deployment mit RollingUpdate 
    - status \<deployment>
    - undo 
  - **run**
    - Pod starten (imperativ) 
    - `run <podname> --image=<image> [-it] -- /bin/sh -c "..."`
  - **top**
- <https://kubernetes.io/docs/reference/kubectl/>


## YAML-Konfigurationsdateien
- <https://kubernetes.io/docs/concepts/workloads/controllers/>
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
