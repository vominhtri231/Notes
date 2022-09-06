# Kubectl

## Namespace

By default `kubectl` will execute in the defautl namespace, to execute on different namespace, we need to either:

- Set specific namespace on each command via `-n <namespace>` flag.
- Set context's namespace via:  
 `kubectl config set-context --current --namespace=<namespace>`

## Handle resources in imperative style

* To generate the yml file from the imperative stype command, use flag `-o yml`
* To not apply the change but for observing the protential changes on the client side, use flag `--dry-run `; for server side (which will compare command with the server's resource ), use flag `--server-dry-run`

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

### Run

Run a pod, this is useful when create a pod for debugging or troubleshouting

```sh
kubeclt run --image=nginx
```

## Handle resources in declarative style

This required yaml files with predefined structure.

```sh
kubectl apply -f <yaml-file>
kubectl apply -f <folder>/
kubectl apply -f https://abc/def.yaml

# For specifing the differences between the server resources and the yaml file 
kubectl diff -f <yaml-file>

# For sepecifing the action explicitly for the resurce, this is not recommended for automation
kubectl delete -f <yaml-file>
kubectl create -f <yaml-file>
kubectl update -f <yaml-file>
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
kubectl logs -f <pod-id> # for live log
kubectl logs <pod-id> --previous # for log in ended pod
kubectl exec -it <pod-id> -- <path-to-executable>

kubectl logs nginx-depl-12345-678
kubectl exec -it nginx-depl-12345-678 -- /bin/sh
```

### Copy file from/to pod

```sh
kubectl cp <file-src> <file-dest>

kubectl cp <namespace>/<pod>:<path-in-pod> <path-local>
kubectl cp <path-local> <namespace>/<pod>:<path-in-pod>
```

Note: should copy from the working dir in the pod
