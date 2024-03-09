https://spinnaker.io/docs/setup/quickstart/

https://github.com/armory/spinnaker-operator


Install
- minikube https://minikube.sigs.k8s.io/docs/
- kubectl https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
- spinnaker 


```shell
minikube start

# Pick a release from https://github.com/armory/spinnaker-operator/releases (or clone the repo and use the master branch for the latest development work)
mkdir -p spinnaker-operator && cd spinnaker-operator
bash -c 'curl -L https://github.com/armory/spinnaker-operator/releases/latest/download/manifests.tgz | tar -xz'
 
# Install or update CRDs cluster wide
kubectl apply -f deploy/crds/

# Install operator in namespace spinnaker-operator, see below if you want a different namespace
kubectl create ns spinnaker-operator
kubectl -n spinnaker-operator apply -f deploy/operator/cluster
```
