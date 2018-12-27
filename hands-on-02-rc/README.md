# Hands-on 02 | Replication Controllers (RC)

## Create a namespace and set as current

```bash
kubectl apply -f 00-namespace.yaml
kubectl config use-context KubeCluster
kubectl config set-context KubeCluster --namespace=hands-on-2
```

## Create a replication controller with imperative way (not recommended and deprecated way way)

There is no way to create a single rc with iterative way. We can run this command below (it's very similar to `hands-on-01`, the only difference is `--replicas=n` statement)

```bash
kubectl run server2 --replicas=3 --image=sadedil/simpleinfoserver:latest # server2 is just an alias

# To delete these objects created by `kubectl run`, you should delete deployment
kubectl delete deploy server2 # server2 is the name of the deployment we've just created
```

## Create a replication controller with declarative way (recommended way)

This will create a rc and three pods (three isn't the magic number, it's defined in `01-rc.yaml`)
```bash
# Create
kubectl apply -f 01-rc.yaml

# To delete the newly created rc and linked pods
kubectl delete -f 01-rc.yaml
```

## About the links between replication controller and pods
The manifest file named `01-rc.yaml` creates a rc and pods. But how these different objects linked together?

All relation between rc and pods provided by the labels. If we try to create another pod with the label `app=my-label-1`, we can't succeed. Because the desired state declared in the `01-rc.yaml` will try to fix running container count to 3. So it will terminate the new pod immediately.

To see this story in action we can run this line.
```bash
kubectl apply -f 02-proof-of-desired-state.yaml
```

`kubectl` will say `pod/pod-temp created` but we will see no pod running in dashboard (you can get running pods with this command `kubectl get pods`).

If we change the `app` label's value different from the `my-label-1`, a new pod will created. But this new pod won't have any relation with our replication controller. It will be independent.