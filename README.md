# AsciiArtify
## Comparison of Kubernetis cluster tools for local development and testing

### Minikube
Local Kubernetes system which allows to deploy Kubernetes cluster on one computer

- `OS and Architectures support`
Supports Linux, MacOS and Windows and different architectures.
- `Automation capability`
Allows to automate deployment process with scripts
- `Additional features`
Monitoring and cluser management

### Kind
Tool which allows to create local Kubernetes clusters in Docker container

- `OS and Architectures support`
Supports Linux, MacOS and Windows and but limited number of architectures.
- `Automation capability`
Deploy multinode clusters on one computer
- `Additional features`
Integration with CI/CD

### k3d
Tool for creating local Kubernetes clusters in Docker containers with Rancher Kubernetes Engine (RKE). 

- `OS and Architectures support`
Supports OSes which support Docker.
- `Automation capability`
Allows the creation of local Kubernetes clusters in Docker containers.
- `Additional features`
Lightweight and quick tool for deploying cluster


|                                | **Minikube**                                     | **Kind**                                         | **k3d**                                          | **Podman**                                       |
|--------------------------------------------------|--------------------------------------------------|--------------------------------------------------|--------------------------------------------------|--------------------------------------------------|
| **Pros**                                      | + Easy to use<br> + Good documentation and community support | + Works within Docker containers |  + Works within Docker containers<br>+ Fast cluster creation and testing | + Easy to use<br>+ Works within Docker containers<br>+ Light alternative to Docker 
| **Cons**                                      | - Doubts about scalability<br> - Time for configuration | - Limited information on scalability<br>- Limited community documentation<br>- Less functions than in Minikube | - Limited documentation<br>- Potential scalability concerns | - Limited information on scalability<br>- Limited community documentation |


![K3D Demo](k3d.gif)

![Kind Demo](kind.gif)

![Minikube Demo](minikube.gif)
