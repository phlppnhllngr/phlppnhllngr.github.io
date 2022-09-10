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
- **Rancher Desktop**
  - *an open-source desktop application for Mac, Windows and Linux. It provides Kubernetes and container management. You can choose the version of Kubernetes you want to run. You can build, push, pull, and run container images. The container images you build can be run by Kubernetes immediately without the need for a registry.*
  - *leverages proven projects to do the dirty work. That includes containerd, k3s, kubectl, and more*
  - *On MacOS and Linux, Rancher Desktop leverages a virtual machine to run containerd and Kubernetes. Windows Subsystem for Linux v2 is leveraged for Windows systems.*
  - *provides container management and Kubernetes on the desktop*
  - *After Rancher Desktop is installed, users will have access to these supporting utilities: Helm, kubectl, nerdctl, Moby, Docker Compose*
  - *requires Windows Subsystem for Linux on Windows; this will automatically be installed as part of the Rancher Desktop setup*
  - <https://docs.rancherdesktop.io/>
 
### Lokal entwickeln
<img src="https://www.jambit.com/site/assets/files/10220/minikube-kind-k3s-local-kubernetes-cluster-1.-squaremedium.jpg" loading="lazy"/><br/>
- **minikube**
  - *Like kind, minikube is a tool that lets you run Kubernetes locally. runs a single-node Kubernetes cluster on your personal computer*
  - *Minikube is the officially supported way to run Kubernetes locally on macOS, Windows, or Linux. Furthermore, it is the only tool that is a drop-in replacement for Docker Desktop.* (<https://matt-rickard.com/docker-desktop-alternatives/>)
  - *Ansatz: Es wird eine VM [Windows: HyperV oder VirtualBox] erzeugt, die im Wesentlichen ein K8s-Cluster mit einer Node ist.*
  - *test local cluster setup where master processes and worker processes run on one node*
  - *node runs in virtual box*
  - *installs kubectl and docker runtime*
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
  - <https://github.com/kubernetes/minikube> *24.7k
  - <https://minikube.sigs.k8s.io/docs/>
  - <https://kubernetes.io/docs/tutorials/hello-minikube/>
- **kind**
  - *lets you run Kubernetes on your local computer*
  - Cluster in Docker-Container (keine VM wie bei minikube)
  - *tool for running local Kubernetes clusters using Docker container "nodes"*
  - <https://kind.sigs.k8s.io/docs/>
- **K3s**
  - *Lightweight Kubernetes*
  - *Production ready, easy to install, half the memory, all in a binary less than 100 MB.*
  - *single binary, wraps Kubernetes and other components in a single, simple launcher*
  - *offers a VM based Kubernetes environment*
  - *is designed for use in production, which makes it one of the best options to simulate a real production environment locally*
  - <https://github.com/k3s-io/k3s> *20.9k
  - <https://k3s.io/>
- **k3d**
  - *Little helper to run CNCF's k3s in Docker*
  - *k3s is the lightweight Kubernetes distribution by Rancher*
  - *you can spin up a multi-node k3s cluster on a single machine using docker*
  - <https://github.com/k3d-io/k3d> *3.8k
  - VSC-Plugin: <https://github.com/inercia/vscode-k3d>
  - GUI: <https://github.com/inercia/k3x>
- **MicroK8s**
  - *small, fast, single-package Kubernetes for developers, IoT and edge.*
  - *Perfect for: Developer workstations IoT Edge CI/CD*
  - *Unlike miniKube, microK8S can run multiple nodes in the local Kubernetes cluster*
  - <https://github.com/canonical/microk8s> *6.7k
- <https://yankee.dev/6-tools-to-run-kubernetes-locally>
- <https://www.jambit.com/aktuelles/toilet-papers/minikube-vs-kind-vs-k3s-welches-lokale-kubernetes-cluster-eignet-sich-am-besten/>
