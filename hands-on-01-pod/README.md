# Hands-on 01 | Pods

## Create a namespace

```bash
kubectl create ns hands-on-1-pod # Imperative
kubectl apply -f 00-namespace.yaml # Declarative (do the same thing as above)
```

> `KubeCluster` is the name of the cluster

## Set the current namespace
```bash
# Use the recently created namespace
# KubeCluster is context name
kubectl config use-context KubeCluster
kubectl config set-context KubeCluster --namespace=hands-on-1-pod
```

## Create a pod with imperative way (not recommended and deprecated way)

This will create a deployment, replica set and pods for us

```bash
kubectl run pod1 --image=sadedil/simpleinfoserver:latest # pod1 is just an alias

# To delete these objects created by `kubectl run`, you should delete deployment
kubectl get deployments # get the name
kubectl delete deploy pod1 # pod1 is the name
```

If we want to create a pod without deployment and replica set we can add `--restart=Never` argument. The default value of `restart` is `Always`.

```bash
# To create single pod
kubectl run pod1 --image=sadedil/simpleinfoserver:latest --restart=Never
```

## Create a pod with declarative way (recommended way)
To create a pod with manifest file we will use `kubectl apply`. This will only create a pod object, not Deployment, not Replica Set

>Also we can use `create` instead of `apply`, but `create` will not work when trying to update object, but `apply` works

```bash
# Create
kubectl apply -f 01-pod.yaml

# To delete the newly created pod and the namespace
kubectl delete -f 01-pod.yaml
kubectl delete -f 00-namespace.yaml
```