# Learning Kubernetes
To run this examples:

## For simple nginx pod definition
```
kubectl create -f pod-definition-nginx.yml
```

To delete the created pod

```
kubectl delete -f pod-definition-nginx.yml
```

## For a "production" nginx pod definition
```
kubectl create -f pod-definition-nginx-prod.yml
```

To delete the created pod
```
kubectl delete -f pod-definition-nginx-prod.yml
```

## For a replica controller with 5 pods instances running
```
kubectl create -f replication-controller.yml
kubectl get replicationcontroller
kubectl get pods -o wide
```

To delete them

```
kubectl delete -f replication-controller.yml
```