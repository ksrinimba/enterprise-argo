<p align="center">
	<img src="https://github.com/OpsMx/enterprise-argo/blob/main/img/opsmx.png" width="20%" align="center" alt="OpsMx">
</p>

# OpsMx Enterprise for Argo

For more information, visit https://www.opsmx.com

## Setup Instructions

### Prerequisites

- Kubernetes cluster 1.20 or later with at least 4 cores and 16 GB memory
- Helm 3 is setup on the client system with 3.10.3 or later
  ```console
  helm version
  ```
  If helm is not setup, follow <https://helm.sh/docs/intro/install/> to install helm.

### Installing the ISD-ARGO

- Add opsmx helm repo to your local machine

   ```console
   helm repo add isdargo https://opsmx.github.io/enterprise-argo/
   ```

  Note: If opsmx helm repo is already added, do a repo update before installing the chart

   ```console
   helm repo update
   ```

- Your Kubernetes cluster shall support persistent volumes

- It is assumed that an nginx ingress controller is installed on the cluster, by default ingress resources are created for oes-ui, argocd and argo-rollouts services. Customize the hosts for ISD-ARGO using the options in the values.yaml under oesUI, argocd, argorollouts . If any other ingress controller is installed, set createIngress flag to false and configure your ingress.

  Instructions to install nginx ingress
  https://kubernetes.github.io/ingress-nginx/deploy/

  Instructions to install cert-manager
  https://cert-manager.io/docs/installation/kubernetes/

- Helm v3 expects the namespace to be present before helm install command is run. If it does not exists,

  ```console
  kubectl create namespace opsmx-argo
  ```
- There are different flavours for Installing ISD-ARGO

    Values yamls    | Description 
  --------------| ----------- 
  isd-argo-minimal-values.yaml | This file is used for Installing ISD,Argo CD and Argo Rollouts 
  isd-minimal-values.yaml | This file is used for Installing ISD without Argo CD and Argo Rollouts 
  isd-rollouts-values.yaml | This file is used for Installing ISD and Argo Rollouts without Argo CD
  onlyargorollouts-values.yaml | This file is used for Installing only Argo Rollouts without Argo CD and ISD
  argocd-rollouts-values.yaml | This file is used for Installing Argo CD and Argo Rollouts without ISD
 
- Use below command to install the helm chart:

  ```console
  helm install isdargo isdargo/isdargo -f isd-argo-minimal-values.yaml -n opsmx-argo --timeout 15m
  ```

The command deploys ISD-ARGO on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

### Uninstalling the Chart

To uninstall/delete the deployment:

  ```console
  helm uninstall isdargo -n opsmx-argo
  ```
