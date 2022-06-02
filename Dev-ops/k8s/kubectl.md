# Kubectl

## Namespace

By default `kubectl` will execute in the defautl namespace, to execute on different namespace, we need to either:

- Set specific namespace on each command via `-n <namespace>` flag.
- Set context's namespace via:  
 `kubectl config set-context --current --namespace=<namespace>`

## Handle resources

### Create

```sh
kubectl create <resource-type> <name> [options]

kubectl create deployment nginx-depl --image=nginx
```

### Get

```sh
kubectl get <resource-type>
kubectl describe <resource-type> <name>

kubectl get deployment
kubectl decribe deployment nginx-depl
```

### Edit

```sh
kubectl edit <resource-type> <name>

kubectl edit deployment nginx-depl
```

### Delete

```sh
kubectl delete <resource-type> <name>

kubectl delete deployment nginx-depl
```

## Handle pod

### Scale

```sh
kubectl scale deployment <deployment-name> --replicas=<number>
```

### Restart

This command will kill one pod at a time, then scale up a new pod util all pods are newer.

```sh
kubectl rollout restart deployment <deployment-name>
```

### Debug

```sh
kubectl logs <pod-id>
kubectl exec -it <pod-id> -- <path-to-executable>

kubectl logs nginx-depl-12345-678
kubectl exec -it nginx-depl-12345-678 -- /bin/sh
```

## Apply configuration file

```sh
kubectl apply -f <yaml-file>
kubectl delete -f <yaml-file>
```
