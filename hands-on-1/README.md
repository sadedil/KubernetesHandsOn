# Hands-on 1

Create a namespace, and use it
```bash
####### Imperative ######
kubectl create ns hands-on-1

####### Declarative ######
kubectl apply -f 00-namespace.yaml

# Use the recently created namespace
# KubeCluster is context name
kubectl config set-context KubeCluster --namespace=hands-on-1
```

Create a pod with imperative way (not recommended way)
```bash
####### Imperative ######

# This  will create a deployment, replica set and pods for you
# server1 is just an alias
kubectl run server1 --image=sadedil/simpleinfoserver:latest

# To delete these objects created by `kubectl run`, you should delete deployment
kubectl get deployments # get the name
kubectl delete deploy server1 # server1 is the name
```

Create a pod with declarative way (recommended way)
```bash
####### Declarative ######

# To create a pod with manifest file we cb use apply
# This will only create a pod object, not Deployment, not Repica Set
# (Also we can use `create` instead of `apply`, but `create` will not work when trying to update, but `apply` works)
kubectl apply -f 01-pod.yaml

# To delete create pod
kubectl delete -f 01-pod.yaml
```