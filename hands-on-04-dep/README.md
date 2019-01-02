# Hands-on 04 | Deployments (DEP)

## As always create a namespace and set as current

```bash
kubectl apply -f 00-namespace.yaml
kubectl config use-context KubeCluster
kubectl config set-context KubeCluster --namespace=hands-on-4-dep
```

> `KubeCluster` is the name of the cluster

## Create a deployment with imperative way

> When we use `kubectl run ...` command, actually we are creating a deployment with imperative way as we seen in `hands-on-01-pod`, so we don't need the mention here again.

## Create a deployment with declarative way

```bash
# Create deployment and a serivce
kubectl apply -f 01-dep.yaml
```

Up to this point, there is no magic. The command above will create a `deployment`, a `replica set` (!) and `pod`s. Let's update our app to version 2.0.0.

I've prepared a new file `02-dep-v2.yaml`. It's almost same with `01-dep.yaml`. The only difference is this line:
```yaml
...
image: sadedil/simpleinfoserver:2.0.0 # old one was 1.0.0
...
```

Let's apply the update
```bash
kubectl apply -f 02-dep-v2.yaml
```

This command will start creating new containers and terminating old ones until the actual state equals the desired state. This is the default update strategy: `RollingUpdate`.

According to this story there must be no downtime, but Kubernetes actually doesn't know when our containers ready to accept requests. Hence, we will add some probing to our deployment.

Let's make our deployment more robust (zero downtime)
```bash
kubectl apply -f 03-dep-zero.yaml
```


# ... to be continued


```bash
# To delete all resources in yaml file
kubectl delete -f 01-dep.yaml
```