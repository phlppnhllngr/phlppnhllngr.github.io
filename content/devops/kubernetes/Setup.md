---
title: Setup
parent: Kubernetes
grand_parent: DevOps
---

# Setup

## Tools
- **kubeadm**
  - *create and manage Kubernetes clusters*
  - <https://kubernetes.io/docs/admin/kubeadm/>

 
### Lokal entwickeln
<img src="https://www.jambit.com/site/assets/files/10220/minikube-kind-k3s-local-kubernetes-cluster-1.-squaremedium.jpg" loading="lazy"/><br/>
- **Docker Desktop**
  - hat Support für <mark>Single-Node-Cluster</mark> (Optionen -> Enable Kubernetes)
  - Support für Mult-Node: <https://github.com/docker/roadmap/issues/312>
- **Rancher Desktop**
  - *an open-source desktop application for Mac, Windows and Linux. It provides Kubernetes and container management. You can choose the version of Kubernetes you want to run. You can build, push, pull, and run container images. The container images you build can be run by Kubernetes immediately without the need for a registry.*
  - *leverages proven projects to do the dirty work. That includes containerd, k3s, kubectl, and more*
  - *On MacOS and Linux, Rancher Desktop leverages a virtual machine to run containerd and Kubernetes. <makr>Windows Subsystem for Linux</mark> v2 is leveraged for Windows systems.*
  - *provides container management and Kubernetes on the desktop*
  - *After Rancher Desktop is installed, users will have access to these supporting utilities: Helm, kubectl, nerdctl, Moby, Docker Compose*
  - *requires Windows Subsystem for Linux on Windows; this will automatically be installed as part of the Rancher Desktop setup*
  - containerd oder dockerd wählbar
    - *[dockerd] allows Rancher Desktop to function as a drop-in replacement for Docker Desktop in many cases*
    - *You cannot run both Docker Desktop and Rancher Desktop (in dockerd mode) simultaneously*
  - 8GB RAM, 4 CPUs
  - derzeit (03/22) kein Corporate-Proxy-Support (<https://github.com/rancher-sandbox/rancher-desktop/issues/4013>)
  - <https://github.com/rancher-sandbox/rancher-desktop> <img loading="lazy" src="https://img.shields.io/github/stars/rancher-sandbox/rancher-desktop?style=flat-square">
  - <https://docs.rancherdesktop.io/>
- **minikube**
  - *Like kind, minikube is a tool that lets you run Kubernetes locally. runs a ~~<mark>single-node</mark>~~ Kubernetes cluster on your personal computer* (mittlerweile wohl auch <mark>Multi-Node</mark> möglich)
  - *Minikube is the officially supported way to run Kubernetes locally on macOS, <mark>Windows</mark>, or Linux. Furthermore, it is the only tool that is a drop-in replacement for Docker Desktop.* (<https://matt-rickard.com/docker-desktop-alternatives/>)
  - *Ansatz: Es wird eine VM [Windows: HyperV oder VirtualBox] erzeugt, die im Wesentlichen ein K8s-Cluster ~~mit einer Node~~ ist.*
  - *test local cluster setup where master processes and worker processes run ~~on one node~~*
  - *installs kubectl and docker runtime*
  - 2GB RAM, 2 CPUs, 20GB HDD, Docker Desktop nicht notwendig
  - CLI commands
    - addons
      - *minikube includes a set of built-in addons that can be enabled, disabled and opened in the local Kubernetes environment.*
      - disable $addon
      - enable $addon
        - `minikube addons enable metrics-server`
      - list
        - listet Addons (enabled & disabled)
    - delete
      - *delete the Minikube VM*
    - start
      - `minikube start --vm-driver=<driver> [--alsologtostderr]`
    - stop
      - *stop the Minikube virtual machine*
    - status
      - Status von Host, kubelet, api server einsehen
    - dashboard
  - *minikube is for starting and deleting the cluster, for everything else use kubectl*
  - Drivers: Docker, VirtualBox, Podman, ... (<https://minikube.sigs.k8s.io/docs/drivers/>)
  - <https://github.com/kubernetes/minikube> <img loading="lazy" src="https://img.shields.io/github/stars/kubernetes/minikube?style=flat-square">
  - <https://minikube.sigs.k8s.io/docs/>
  - <https://kubernetes.io/docs/tutorials/hello-minikube/>
- **kind**
  - [K]ubernetes [in] [D]ocker 
  - <mark>Multi-Node</mark>, erfordert Docker 
  - *lets you run Kubernetes on your local computer*
  - Cluster in Docker-Container (keine VM wie bei minikube)
  - *tool for running local Kubernetes clusters using Docker container "nodes"*
  - <mark>Windows: ja</mark>
  - Setup
    - exe downloaden, in kind.exe umbenennen, zum PATH hinzufügen
    - Docker starten
    - ```
      kind create cluster
      kubectl cluster-info --context kind-kind
      kind delete cluster
      ```
    - by Default erzeugt `kind create cluster` ein Cluster mit nur einer Node, um mehrere Nodes zu bekommen siehe `kind-config.yaml` <br/>
      <https://mcvidanagama.medium.com/set-up-a-multi-node-kubernetes-cluster-locally-using-kind-eafd46dd63e5>
    - ```
      cd C:\Apps\kind
      kind create cluster --name k8s-playground --config kind-config.yaml
      kubectl cluster-info --context kind-k8s-playground
      kubectl get nodes // 1x control plane, 2x worker / oder kind get nodes --name k8s-playground
      docker ps // 3 Container
      docker exec -it k8s-playground-control-plane /bin/sh -c "kubectl cluster-info"
      ```
  - <https://github.com/kubernetes-sigs/kind> <img loading="lazy" src="https://img.shields.io/github/stars/kubernetes-sigs/kind?style=flat-square">
  - <https://kind.sigs.k8s.io/docs/>
- **K3s**
  - *Lightweight Kubernetes*
  - *Production ready, easy to install, half the memory, all in a binary less than 100 MB.*
  - *single binary, wraps Kubernetes and other components in a single, simple launcher*
  - *offers a VM based Kubernetes environment*
  - *is designed for use in production, which makes it one of the best options to simulate a real production environment locally*
  - <mark>kein Windows-Support</mark>: <https://github.com/k3s-io/k3s/issues/114>
  - <https://github.com/k3s-io/k3s> <img loading="lazy" src="https://img.shields.io/github/stars/k3s-io/k3s?style=flat-square">
  - <https://k3s.io/>
- **k3d**
  - *Little helper to run CNCF's k3s in Docker*
  - *one of the apparent differences is that k3s deploys a virtual machine-based Kubernetes cluster while k3d deploys Docker-based k3s Kubernetes clusters*
  - *k3d is more suitable for use in even smaller environments like Raspberry Pi, IoT, and Edge devices.*
  - *k3d appears to be a more flexible and improved version of k3s even though their features and usage are similar.*
  - Windows: ja
  - <https://github.com/k3d-io/k3d> <img loading="lazy" src="https://img.shields.io/github/stars/k3d-io/k3d?style=flat-square">
  - VSC-Plugin: <https://github.com/inercia/vscode-k3d>
  - GUI: <https://github.com/inercia/k3x>
- **MicroK8s**
  - *small, fast, single-package Kubernetes for developers, IoT and edge.*
  - *Perfect for: Developer workstations IoT Edge CI/CD*
  - *Unlike miniKube, microK8S can run <mark>multiple nodes</mark> in the local Kubernetes cluster*
  - <mark>Windows: ja</mark> (Hyper-V oder VirtualBox), 4GB+ RAM, 40GB+ HDD
  - <https://github.com/canonical/microk8s> <img loading="lazy" src="https://img.shields.io/github/stars/canonical/microk8s?style=flat-square">
- <https://yankee.dev/6-tools-to-run-kubernetes-locally>
- <https://www.jambit.com/aktuelles/toilet-papers/minikube-vs-kind-vs-k3s-welches-lokale-kubernetes-cluster-eignet-sich-am-besten/>
