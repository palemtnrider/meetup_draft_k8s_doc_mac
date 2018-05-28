This is a sipmle expressjs app to illustrate draft

## Presentation questions to answer
- Moving parts?
   - Helm
   - Tiller
   - Docker Registry
   - Code scanning accuracy 
   - What about code bases with multiple dirs and should be separate services?
   - Helm repository
- setup your env run ```eval $(minikube docker-env)```
- minikube API version is behind docker (version-wise)
   - makes some cleanup tasks more difficult.  e.g. can run ```docker system prune```
- Execute tests
- Keep an eye on images - each build generates a unique tag which can cause issues
- Where are the docker images stored after being built?
- ```draft connect``` cool key features
- Setting context between minikube and docker-for-desktop
```
$ kubectl config get-contexts
$ kubectl config use-context docker-for-desktop
```
- issue with minikube .0.26.1
```
minikube start --bootstrapper kubeadm
```
or 
```
minikube start --bootstrapper localkube
```


- How to configure the base images
   - go image is pretty large

- How to configure docker to point to minikube
   - requires running the docker edge version
- how to cleanup images
   - in minikube
- Using docker commands to status minikube...
- what is running
   - Docker Edge
   - minikube
   - what VMs?
   - is there a swarm?

- Pause containers to simulate pods...
- Is docker really running k8s or just containers that are k8s?

- Issues I ran into 
   - Tried _watch_ and _auto-connect_ which didn't work.  Turns out _watch_ is pretty buggy and I believe the draft team is going to defer to the IDE integrations to handle
   - Single helm chart per repo.  Needs Dockerfile and charts dir at the root.
   - Error that k8s can't pull the image
      - You are probably missing the minikube settings in your shell - ```eval $(minikube docker-env)``` 

---
Enable kubernetes in Docker edge
   - Note you have to re-install docker if you don't have edge installed

I'm running version - 18.05.0-ce-rc1; kubernetes v1.9.6

View services running
```docker ps```
- *pause* containers - these are used to hang processes off i.e. **PODS** in k8s
- ```docker ps --format "{{.Names}}:{{.Command}}```


Same command in ```kubectl```
- use ```kubectl config get-contexts``` to see the new Docker k8s config
- use ```kubectl config use-context docker-for-desktop``` to switch to the Docker for mac context
- ```kubectl get namespaces``` and ```kubectl get services``` to see namespaces and services
- troubleshooting ```kubectl cluster-info dump```
- run the kubernets dashboard 
```
kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
```
   - open a proxy server to the cluster ```kubectl proxy```
   - hit the dashboard at http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/#!/overview?namespace=default

Now we need the tiller process installed so we can deploy helm charts to our cluster.
- ```helm init```

tried to run helm - docker might not be healthy
- ```2018/05/06 10:13:44 buildApp: buildImg error: Cannot connect to the Docker daemon at tcp://192.168.99.100:2376. Is the docker daemon running?```
   - old shell use ```eval $(docker-machine env --unset)``` to fix

run ```draft up```

run ```draft connect```
   - gives you an IP to hit your new service.

Note that a POD (pause container is created to house your go program)

# Todo:
- import the k8s dashboard into yipee - https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml 

# TODO
- Create yipee.io mode for ChartMuseum, download, add to helm
   - alt is to install the helm chart
   - how to configure the chart for storage?
   - download and run - set service to NodePort
   - add as a repo to helm ```helm repo add cm http://localhost:31144```
   - ```helm repo list```
   - ```helm package .```
   - ```curl --data-binary "@go-v0.1.0.tgz" http://localhost:31144/api/charts```
   - ```helm search cm\``` - doesn't seem to work
   - ```curl http://localhost:31144/api/charts``` should show the chart
   - to install a helm chart into your cluster
      - ```helm install go --repo http://localhost:31144 --name my-go-example``` odd that we can't use the name of the repo 
   - Change the version in Chart.yaml
   - package and push to the repo
   - ```helm upgrade --repo http://localhost:31144 my-go-example go```
   - ```helm history my-go-example```
   - ```helm rollback my-go-example 1```
   - ```helm delete my-go-example```
- pull charts from ChartMuseum
- Config 
   - Where it is stored, what's in it, etc
- helm list "Accepts perl filter syntax?"
- relationship between helm, tiller, draft
- does draft use a chart repo?  If not why? Configure it to do so?

Helm has a default local repo - available view ```helm serve```

Where did draft put the docker image?

What is a toml file?

```draft up``` creates a Dockerfile, builds the image, deploys it to kubernetes.  use ```draft connect``` to setup a proxy to the service

## Example use case
- create the chart, deploy
- update, re-deploy
- rollback



