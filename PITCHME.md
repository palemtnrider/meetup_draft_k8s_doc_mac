### Brief overview of Draft

<br/>Mark Emeis
<br/>Colorado Springs Docker Meetup
<br/>May 30, 2018
---
### Agenda
1. Docker and Kubernetes - great together 
1. Helm 
   * Why do I need it
   * How to setup
   * Example usage
1.  Draft
   * Why do I need it
   * How to setup
   * Example usage
1. Resources

Note:   Minikube can also be used

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
### Notes and Comands
* `docker ps`   _add --format to reduce output_
   * running images
* `kubctl get pods --all-namespaces` 
* `kubectl config get-contexts`
   * ensure you are pointing at the right context
* Pause containers - needed to create _pods_
* Debugging
   * `kubectl cluster-info dump`
   * `docker info`
+++
### Kubernetes Dashboard
- run the kubernets dashboard 
```
kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
```

Open a proxy server to the cluster `kubectl proxy`

Hit the dashboard at http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/#!/overview?namespace=default

---
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
