### Proof of concept for ArgoCD

## Purpose of the document

Argo CD is a declarative, GitOps continuous delivery tool for Kubernetes.
It allows automate the process of application deployment. Application configuration is done in declarative way and stored in Git repository.
Argo CD follows the GitOps pattern of using Git repositories as the source of truth for defining the desired application state. 

## Architecture

1. ![Screenshot of Argo CD architecture.](https://argo-cd.readthedocs.io/en/stable/assets/argocd_architecture.png)

## Installation guide

1. Create K3D cluster 
```bash
$ k3d cluster create argo

INFO[0029] Cluster 'argo' created successfully!         
INFO[0029] You can now use it like this:                
kubectl cluster-info

$ kubectl cluster-info

Kubernetes control plane is running at https://0.0.0.0:46393
CoreDNS is running at https://0.0.0.0:46393/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://0.0.0.0:46393/api/v1/namespaces/kube-system/services/https:metrics-server:https/proxy

$ vi ~/.kube/config

apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: ...
    server: https://0.0.0.0:46393
  name: k3d-argo
contexts:
- context:
    cluster: k3d-argo
    user: admin@k3d-argo
  name: k3d-argo
current-context: k3d-argo
kind: Config
preferences: {}
users:
- name: admin@k3d-argo
  user:
    client-certificate-data: ...
    client-key-data: ...
```    

2. Install ArgoCD
```bash
$ kubectl create namespace argocd
namespace/argocd created

$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
...
customresourcedefinition.apiextensions.k8s.io/appprojects.argoproj.io created
...
serviceaccount/argocd-server created
...
clusterrole.rbac.authorization.k8s.io/argocd-server created
...
rolebinding.rbac.authorization.k8s.io/argocd-server created
...
service/argocd-server created
...
deployment.apps/argocd-server created
...
networkpolicy.networking.k8s.io/argocd-server-network-policy created

$ kubectl get pods -n argocd
argocd-redis-66d9777b78-lp52h                       1/1     Running   0          4m40s
argocd-notifications-controller-6b66d47b45-bxfhj    1/1     Running   0          4m40s
argocd-applicationset-controller-6c8fbc69b5-9wmj7   1/1     Running   0          4m40s
argocd-server-5d8d58455f-6fqw9                      1/1     Running   0          4m39s
argocd-application-controller-0                     1/1     Running   0          4m39s
argocd-dex-server-59bd76d76-qjx6w                   1/1     Running   0          4m40s
argocd-repo-server-b9957974f-jnzfr                  1/1     Running   0          4m39s
```

3. Setup access to ArgoCD GUI

Use method with Port forwarding from Argo CD instruction
```bash
$ kubectl port-forward svc/argocd-server -n argocd 8080:443
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
Handling connection for 8080
```

In order to work on GitHub Codespaces Http protocol should be changed to Https in Ports tab:
![Screenshot of Github port forwarding.](.img/GitHubPortForwarding.png)

Use kubectl command to get named secret and decode it with Base64 gives a password. Login using it on Argo CD UI. 
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

![+ NEW APP](.img/ArgoNewApp.png)

Set Application Name to 'asciiartify'

Set project as default

![+ NEW APP](.img/NewAppConfigs.png)

Specify Repository URL with application which has Kubernetes manifests

Leave default cluster URL

![+ NEW APP](.img/AppStatus.png)

After creation application status is displayed as OutOfSync

![+ NEW APP](.img/AppSynced.png)

To get detailed information open created application. You can see hierarchical structure of the application.
