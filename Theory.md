# Kubernetes: Replication Controller

Controllers are the brain behind k8s they monitor objects and respond accordingly, on scenarios where the application crashes and the pod fails, the replication controller makes sure that there are always running the number of pods specified

The replication controllers also are useful to create multiple pods to balance the load across all pod, replication controllers can manage pods across multiple clusters, (it spans pods across multiple nodes in the cluster), it also scales the application when the demand increases.

Replica Set is not the same as Replica Controller even when they have the same purpose, Replica Set is the new recommended way to set replication, Replica Set is the technology replacing the older one Replica Controller.

The main difference between the replica set and the replica controller is that the replica set contains a selector, that helps the replica set identify what pods fall under it because replica sets also can manage pods that were not created as part of the replica set creation, if there are pods created before the replica set creation that match the labels specification of the replica set, then the replica set will also affect pods when creating the replicas

The selector also is available for the replica controller, when not defined, it assumes is the same as the labels defined at the pod

The labels are the filters for replica sets to know what pods to monitor among all pods running in a cluster, the label, the label defined at the pod, for replica sets the pod definition is under spec.template.meta

kubectl replace -f replicaset.yml after changing the number of replicas at the yml file will scale up or down the number of running pods

kubectl useful commands for replicaset:

create, get, delete, replace, scale

```bash
kubectl create -f replicaset.yml
kubectl get replicaset
kubectl delete replicaset myapp-replicaset
kubectl delete replicaset -f replicaset.yml
kubectl replace -f replicaset-definition.yml
kubectl scale -replicas=6 -f replicaset.yml
``` 

If a pod is deleted with ```kubectl delete pod <podname>```
Kubernetes will replace the deleted pod "immediatly",  ```kubectl get pods```
will show that a container is in status Terminating and anotherone will be in state ContainerCreating, after creating the replica if ```kubectl create -f pods/pod-definition-nginx.yml``` the replica set will delete it since there shouldn't be more than 3 pods running with that label according to that replica set.

kubectl describe replicaset will provide some information related to that replicaset, stuff like

```Replicas:     3 current / 3 desired
Pods Status:  3 Running / 0 Waiting / 0 Succeeded / 0 Failed
```
and will have logs of the events, showing that there was an extra pod and needed to be deleted

```
  Type    Reason            Age              From                   Message
  ----    ------            ----             ----                   -------
  Normal  SuccessfulCreate  6m               replicaset-controller  Created pod: someapp-replicaset-bc2tn
  Normal  SuccessfulCreate  6m               replicaset-controller  Created pod: someapp-replicaset-msm8m
  Normal  SuccessfulCreate  6m               replicaset-controller  Created pod: someapp-replicaset-tswlz
  Normal  SuccessfulCreate  5m               replicaset-controller  Created pod: someapp-replicaset-4xwvs
  Normal  SuccessfulDelete  2s (x2 over 2m)  replicaset-controller  Deleted pod: someapp-pod
```

To destroy the replica set ```kubectl delete replicaset some-app```