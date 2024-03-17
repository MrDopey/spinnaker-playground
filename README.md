https://spinnaker.io/docs/setup/quickstart/

https://github.com/armory/spinnaker-operator

https://gist.github.com/jhoughtelin/e31ceeb1aa48330775864f9c58a921f5

Install
- minikube https://minikube.sigs.k8s.io/docs/
- kubectl https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
- spinnaker 


```shell
minikube start  --kubernetes-version=v1.25.0

# Pick a release from https://github.com/armory/spinnaker-operator/releases (or clone the repo and use the master branch for the latest development work)
mkdir -p spinnaker-operator && cd spinnaker-operator
bash -c 'curl -L https://github.com/armory/spinnaker-operator/releases/latest/download/manifests.tgz | tar -xz'
 
# Install or update CRDs cluster wide
kubectl apply -f deploy/crds/

# Install operator in namespace spinnaker-operator, see below if you want a different namespace
kubectl create ns spinnaker-operator
kubectl -n spinnaker-operator apply -f deploy/operator/cluster
```

The spinnaker operator only watches the CRD in it's own namespace
```shell
kubectl apply -f deploy/crds/
kubectl create ns spinnaker-operator
kubectl apply -n spinnaker-operator -f deploy/operator/basic
kubectl create ns spinnaker-operator
kubectl -n spinnaker-operator apply -f deploy/spinnaker/basic/spinnakerservice.yml
```

Once everything is running
```shell
kubectl -n spinnaker-operator port-forward deployment/spin-deck 9000:9000
kubectl -n spinnaker-operator port-forward deployment/spin-gate 8084:8084
```

# TODO 

Fix spin-front, it's connecting to a non-existing aws instance

