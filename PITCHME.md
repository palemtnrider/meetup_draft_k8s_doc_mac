### Brief overview of Draft

<br/>Mark Emeis
<br/>Colorado Springs Docker Meetup
<br/>May 30, 2018
---
### Agenda
1. Docker and Kubernetes - great together 
   * Minikube as an alternative 
1. Helm 
   * Why do I need it
   * How to setup
   * Example usage
1.  Draft
   * Why do I need it
   * How to setup
   * Example usage
1. Resources
---
#### Docker and Kubernetes
* Requires the edge channel 
* Preferences > Kubernetes
   * Enable Kubernetes
   * Show system containers 
![K8s setup](images/docker-config-k8s.png)
+++
#### Docker and Kubernetes
* Preferences > Advanced
   * Allocate additional memory 
![Advanced setup](images/docker-config-adv.png)
+++
### 
* docker ps vs kubctl get 
### Helm


---
### Tiller (server component)
Server part of helm - manages packages inside the cluster

---
### Helm mesuem 

---
### Draft

Note:
Each build creates an image; 
---
### Resources
* [Docker mac edge channel](https://docs.docker.com/docker-for-mac/edge-release-notes/)
* [Helm](https://helm.sh/)
* [Draft](https://github.com/Azure/draft)
* [Chart Museum](https://github.com/kubernetes-helm/chartmuseum)
* [Public helm charts](https://github.com/kubernetes/charts)
