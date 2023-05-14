---
title: Kubernetes
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
