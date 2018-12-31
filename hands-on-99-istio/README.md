# Hands-on 99 | Istio

## As always create a namespace and set as current

```bash
kubectl apply -f 00-namespace.yaml
kubectl config use-context KubeCluster
kubectl config set-context KubeCluster --namespace=hands-on-3
```

> `KubeCluster` is the name of the cluster

## Create a service with imperative way (not recommended way)
