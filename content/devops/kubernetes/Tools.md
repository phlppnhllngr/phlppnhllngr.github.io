---
title: Tools
parent: Kubernetes
grand_parent: DevOps
---

# Tools
- docker-desktop → Docker/Tools
- **Helm**
  - <https://helm.sh>
  - <https://github.com/helm/helm> <img loading="lazy" src="https://img.shields.io/github/stars/helm/helm?style=flat-square">
  - *The package manager for Kubernetes*
  - *Helm is the best way to find, share, and use software built for Kubernetes.*
  - *Helm Charts help you define, install, and upgrade even the most complex Kubernetes application*
  - Begriffe
    - Chart
      - *bundle of templated yaml files* 
    - Config Values
    - Release
      - *running instance of chart combined with configured values*
  - CLI
    - <https://github.com/helm/helm/releases>
    - create
      - Scaffolding für neuen Chart 
      - `helm create <chart-name>`
    - install
      - lädt Chart und startet Anwendung (Deployments, ...) 
      - `helm install <release-name> <identifier> --version <version> [-n <namespace>]`, z. B. `helm install my-prometheus prometheus-community/prometheus --version 15.9.2` 
    - list
      - alias "ls" 
      - Liste der helm-Releases 
      - `helm list [--all-namespaces]`
    - repo
      - add 
        - `helm repo add <name> <url>`
      - list
      - update
    - rollback
    - search
      - hub 
        - `helm search hub <name>` name z. B. "prometheus"
      - repo
    - status
      - `helm status <release>` 
    - uninstall
    - upgrade
  - Helm Dashboard
    - <https://github.com/komodorio/helm-dashboard> <img loading="lazy" src="https://img.shields.io/github/stars/komodorio/helm-dashboard?style=flat-square">
  - Artifacthub
    - <https://artifacthub.io/>
  - helm unittest
    - *BDD styled unit test framework for Kubernetes Helm charts as a Helm plugin.* 
    - <https://github.com/helm-unittest/helm-unittest>
  - Testkube
    - *allows you to automate the executions of your existing testing tools inside your Kubernetes cluster, removing all the complexity from your CI/CD pipelines.* 
    - <https://github.com/kubeshop/testkube> 
- **lens**
  - wie Portainer aber für K8s
  - Binaries von hier laden: <https://github.com/MuhammedKalkan/OpenLens>
  - <https://github.com/lensapp/lens> <img loading="lazy" src="https://img.shields.io/github/stars/lensapp/lens?style=flat-square">
- **kompose**
  - *go from Docker Compose to Kubernetes*
  - *takes a Docker Compose file and translates it into Kubernetes resources*
  - <https://github.com/kubernetes/kompose> <img loading="lazy" src="https://img.shields.io/github/stars/kubernetes/kompose?style=flat-square">
- **argo-cd**
  - *Declarative continuous deployment for Kubernetes.*
  - <https://github.com/argoproj/argo-cd> <img loading="lazy" src="https://img.shields.io/github/stars/argoproj/argo-cd?style=flat-square">
- **pixie**
  - *Instant Kubernetes-Native Application Observability*
  - *Use Pixie to view the high-level state of your cluster (service maps, cluster resources, application traffic) and also drill-down into more detailed views (pod state, flame graphs, individual full-body application requests).*
  - <https://github.com/pixie-io/pixie> <img loading="lazy" src="https://img.shields.io/github/stars/pixie-io/pixie?style=flat-square">
- **kubesphere**
  - *is a distributed operating system for cloud-native application management, using Kubernetes as its kernel*
  - *It provides developer-friendly wizard web UI*
  - <https://github.com/kubesphere/kubesphere> <img loading="lazy" src="https://img.shields.io/github/stars/kubesphere/kubesphere?style=flat-square">
- **kubeapps**
  - *web-based UI for deploying and managing applications in Kubernetes clusters*
  - <https://github.com/kubeapps/kubeapps> <img loading="lazy" src="https://img.shields.io/github/stars/kubeapps/kubeapps?style=flat-square">
- **kubespray**
  - *Deploy a Production Ready Kubernetes Cluster*
  - <https://github.com/kubernetes-sigs/kubespray>
- **telepresence**
  - *Local development against a remote Kubernetes or OpenShift cluster*
  - *You run one service locally, using your favorite IDE and other tools. You run the rest of your application in the [cluster].*
  - *outbound connections will be routed to the cluster. I.e. your laptop is "inside" the cluster.*
  - <https://github.com/telepresenceio/telepresence> <img loading="lazy" src="https://img.shields.io/github/stars/telepresenceio/telepresence?style=flat-square">
- **mizu**
  - *API traffic viewer for Kubernetes enabling you to view all API communication between microservices. Think TCPDump and Wireshark re-invented for Kubernetes*
  - <https://github.com/up9inc/mizu>
- **opencost**
  - *visibility into current and historical Kubernetes spend and resource allocation* 
  - <https://github.com/opencost/opencost>
- **kubescape**
  - *providing a multi-cloud K8s single pane of glass, including risk analysis, security compliance, RBAC visualizer and image vulnerabilities scanning*
  - *scans K8s clusters, YAML files, and HELM charts, detecting misconfigurations according to multiple frameworks, software vulnerabilities, and RBAC (role-based-access-control) violations at early stages of the CI/CD pipeline, calculates risk score instantly and shows risk trends over time* 
  - <https://github.com/kubescape/kubescape>
- **Tanzu Community Edition**
  - free 
  - *no longer an actively maintained project. Code is available for historical purposes only.* 
  - <https://github.com/vmware-tanzu/community-edition>
  - [YT - VMware Tanzu Community Edition Installation and creating an unmanaged Kubernetes cluster](https://www.youtube.com/watch?v=dEMuiagEAg4)
- **Tanzu Kubernetes Grid**
  - <https://tanzu.vmware.com/kubernetes-grid>
- **Tanzu Application Platform**
  - <https://tanzu.vmware.com/developer/tanzu/tap/>
  - [YT - What’s on TAP? Refining Modern Spring Application Development, 02/2023](https://www.youtube.com/watch?v=IY784cDq1E8)
    - Spring Boot + VS Code + TAP  
- **Devtron**
  - *tool integration platform for Kubernetes*
  - *deeply integrates with products across the lifecycle of microservices,i.e., CI, CD, security, cost, debugging, and observability via an intuitive web interface.* 
  - <https://github.com/devtron-labs/devtron>
- **cdk8s**
  - *development framework for defining Kubernetes applications and reusable abstractions using familiar programming languages and rich object-oriented APIs. cdk8s apps synthesize into standard Kubernetes manifests which can be applied to any Kubernetes cluster.*
  - Langs: TS, JS, Python, Java, Go
  - <https://github.com/cdk8s-team/cdk8s> 
  - <https://cdk8s.io/>
- **DevSpace**
  - *Client-Only Developer Tool for Cloud-Native Development with Kubernetes*
  - *Build, test and debug applications directly inside Kubernetes. Develop with hot reloading: updates your running containers without rebuilding images or restarting containers.* 
  - <https://github.com/loft-sh/devspace> <img loading="lazy" src="https://img.shields.io/github/stars/loft-sh/devspace?style=flat-square">
  - [YT - Devspace vs Skaffold: Simplify Java Development in the Kubernetes World By Ana Maria Mihalceanu - 10/2023](https://www.youtube.com/watch?v=Q-jilSBje2A)
- **Skaffold**
  - *command line tool that facilitates continuous development for Kubernetes applications. You can iterate on your application source code locally then deploy to local or remote Kubernetes clusters. Skaffold handles the workflow for building, pushing and deploying your application. It also provides building blocks and describe customizations for a CI/CD pipeline.* 
  - <https://github.com/GoogleContainerTools/skaffold> <img loading="lazy" src="https://img.shields.io/github/stars/GoogleContainerTools/skaffold?style=flat-square">
- **Tanka**
  - *configuration utility for your Kubernetes cluster, powered by the unique Jsonnet language*
  - ```
    local k = import "k.libsonnet";

    {
        grafana: k.apps.v1.deployment.new(
            name="grafana",
            replicas=1,
            containers=[k.core.v1.container.new(
                name="grafana",
                image="grafana/grafana",
            )]
        )
    }
    ```  
  - <https://tanka.dev/>
- **k9s**
  - *provides a terminal UI to interact with your Kubernetes clusters. The aim of this project is to make it easier to navigate, observe and manage your applications in the wild. K9s continually watches Kubernetes for changes and offers subsequent commands to interact with your observed resources.* 
  - <https://github.com/derailed/k9s> <img loading="lazy" src="https://img.shields.io/github/stars/derailed/k9s?style=flat-square">
- **Dashboard**
  - *General-purpose web UI for Kubernetes clusters* 
  - <https://github.com/kubernetes/dashboard> <img loading="lazy" src="https://img.shields.io/github/stars/kubernetes/dashboard?style=flat-square">
- **kube-state-metrics**
  - *listens to the Kubernetes API server and generates metrics about the state of the objects*
  - *It is not focused on the health of the individual Kubernetes components, but rather on the health of the various objects inside, such as deployments, nodes and pods.*
  - *The metrics are exported on the HTTP endpoint /metrics* 
  - <https://github.com/kubernetes/kube-state-metrics> <img loading="lazy" src="https://img.shields.io/github/stars/kubernetes/kube-state-metrics?style=flat-square">
- **kube-score**
  - *performs static code analysis of your Kubernetes object definitions. The output is a list of recommendations of what you can improve to make your application more secure and resilient.*
  - Liste aller Checks: <https://github.com/zegl/kube-score/blob/master/README_CHECKS.md>
  - *can run in your CI/CD environment and will exit with exit code 1 if a critical error has been found*
  - funktioniert auch mit Helm-Charts und Kustomize
  - <https://github.com/zegl/kube-score> <img loading="lazy" src="https://img.shields.io/github/stars/zegl/kube-score?style=flat-square">
- **Velero**
  - *gives you tools to back up and restore your Kubernetes cluster resources and persistent volumes*
  - *Velero consists of: A server that runs on your cluster, a command-line client that runs locally*
  - Volume Backup: <https://velero.io/docs/latest/file-system-backup/#using-opt-in-pod-volume-backup>
  - <https://github.com/vmware-tanzu/velero> <img loading="lazy" src="https://img.shields.io/github/stars/vmware-tanzu/velero?style=flat-square">
- **Argo Workflows**
  - *workflow execution engine for Kubernetes*
  - *implemented as a Kubernetes CRD (Custom Resource Definition)*
  - *Define workflows where each step in the workflow is a container.*
  - <https://github.com/argoproj/argo-workflows/> <img loading="lazy" src="https://img.shields.io/github/stars/argoproj/argo-workflows?style=flat-square"/>
- **Gefyra**
  - *local application development with Kubernetes*
  - <https://github.com/gefyrahq/gefyra> 



## Java
- **Kubernetes & OpenShift Java Client**
  - <https://github.com/fabric8io/kubernetes-client>
- **kubernetes-client/java**
  - <https://github.com/kubernetes-client/java>
- **JKube**
  - *collection of plugins and libraries that are used for building container images using Docker, JIB or S2I build strategies. Eclipse JKube generates and deploys Kubernetes/OpenShift manifests at compile time too.*
  - *also provides a set of tools such as watch, debug, log, etc. to improve your developer experience*
  - <https://github.com/eclipse/jkube>
  - Maven Plugin -> Java/Maven/Plugins/kubernetes
- **Dekorate**
  - *Tools for generating Kubernetes related manifests via annotation processing*
  - Integrations: SpringBoot, Quarkus, Generic Java
  - JUnit-Support
  - <https://github.com/dekorateio/dekorate>
