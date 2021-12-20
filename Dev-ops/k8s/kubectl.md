# Kubectl

## Create

```sh
kubectl create <resource-type> <name> [options]

kubectl create deployment nginx-depl --image=nginx
```

## get resource

```sh
kubectl get <resource-type>
kubectl describe <resource-type> <name>

kubectl get deployment
kubectl get pod
kubectl get replicaset
kubectl decribe deployment nginx-depl
```

## Edit resource

```sh
kubectl edit <resource-type> <name>

kubectl edit deployment nginx-depl
```

## Delete resource

```sh
kubectl delete <resource-type> <name>

kubectl delete deployment nginx-depl
```

## Debug pod

```sh
kubectl logs <pod-id>
kubectl exec -it <pod-id> -- <path-to-executable>


kubectl logs nginx-depl-12345-678
kubectl exec -it nginx-depl-12345-678 -- bin/sh
```

## Apply configuration file

```sh
kubectl apply -f <yaml-file>
kubectl delete -f <yaml-file>
```
