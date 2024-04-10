### Proof of concept for ArgoCD

## Purpose of the document

Argo CD is a declarative, GitOps continuous delivery tool for Kubernetes.
It allows automate the process of application deployment. Application configuration is done in declarative way and stored in Git repository.
Argo CD follows the GitOps pattern of using Git repositories as the source of truth for defining the desired application state. 

## Architecture

1. ![Screenshot of Argo CD architecture.](https://argo-cd.readthedocs.io/en/stable/assets/argocd_architecture.png)

## Installation guide

1. 
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

