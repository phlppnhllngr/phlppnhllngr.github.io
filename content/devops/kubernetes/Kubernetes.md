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
- <u>Commands</u>
  - **apply**
    - *create or update a component (e. g. deployment) from config file [declaratively]*
    - *k8s knows whether to update or create the component*
    - `kubectl apply -f <config-file>`
  - **cluster-info**
  - **config**
    - current-context
    - get-contexts
    - use-context [contextName]
    - view
      - `kubectl config view`
  - **create**
    - `kubectl create -h`
    - mit `--dry-run=client --output yaml --save-config > foo.yaml` können Ressourcen-Yamls erstellt werden
    - deployment
      - *create and run pod and replicaset*
      - `kubectl create deployment <name> --image=<image> [--dry-run] [options]`
      - `kubectl create deployment nginx --image=nginx:latest`
  - **delete**
    - `kubectl delete deployment <deployment>`
    - `kubectl delete -f <config-file>`
  - **describe**
    - `kubectl describe pod <pod>`
  - **edit**
    - *edit deployment configurations*
    - `kubectl edit deployment nginx`
  - **exec**
    - `kubectl exec -it <pod> -- /bin/bash`
  - **expose**
    - `kubectl expose deployment hello-node --type=LoadBalancer --port=8080`
    - *The --type=LoadBalancer flag indicates that you want to expose your Service outside of the cluster.*
    - *On cloud providers that support load balancers, an external IP address would be provisioned to access the Service. On minikube, the LoadBalancer type makes the Service accessible through the `minikube service` command.*
  - **get**
    - `kubectl get nodes|pod|services|deployment|replicaset|events`
  - **logs**
    - `kubectl logs <pod>`
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
