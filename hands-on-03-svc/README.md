# Hands-on 03 | Services (SVC)

## As always create a namespace and set as current

```bash
kubectl apply -f 00-namespace.yaml
kubectl config use-context KubeCluster
kubectl config set-context KubeCluster --namespace=hands-on-3-svc
```

> `KubeCluster` is the name of the cluster

## Create a service with imperative way (not recommended way)

Firstly create three pods has same labels

```bash
kubectl run pod1 --image=sadedil/simpleinfoserver:latest --restart=Never --labels="mykey=myvalue"
kubectl run pod2 --image=sadedil/simpleinfoserver:latest --restart=Never --labels="mykey=myvalue"
kubectl run pod3 --image=sadedil/simpleinfoserver:latest --restart=Never --labels="mykey=myvalue"
```

Then create a service (imperative)
```bash
kubectl expose pod pod1 --type=NodePort --name=service-for-myvalue --labels="mykey=myvalue" --port="80"
```

The newly created service will be linked the three pods, because they are using same labels

> If we run a new pod (pod4) with same labels `mykey=myvalue`, it would be automatically linked again  
If we run a new pod (pod5) with different lables, it would be indepedent

Let's delete three pods and service, we've just created
```bash
kubectl delete pod pod1 pod2 pod3
kubectl delete service service-for-myvalue
```

Then validate no resource remaining in this namespace (`hands-on-3-svc`)
```bash
kubectl get all
```

## Create a service with declarative way (recommended way)

```bash
# Create service and replication controller
kubectl apply -f 01-svc.yaml

# To delete all resources in yaml file
kubectl delete -f 01-svc.yaml
kubectl delete -f 00-namespace.yaml
```