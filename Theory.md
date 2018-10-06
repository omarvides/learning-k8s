# Kubernetes: Replication Controller

Controllers are the brain behind k8s they monitor objects and respond accordingly, on scenarios where the application crashes and the pod fails, the replication controller makes sure that there are always running the number of pods specified

The replication controllers also are useful to create multiple pods to balance the load across all pod, replication controllers can manage pods across multiple clusters, (it spans pods across multiple nodes in the cluster), it also scales the application when the demand increases.

Replica Set is not the same as Replica Controller even when they have the same purpose, Replica Set is the new recommended way to set replication, Replica Set is the technology replacing the older one Replica Controller.


The main difference between the replica set and the replica controller is that the replica set contains a selector, that helps the replica set identify what pods fall under it because replica sets also can manage pods that were not created as part of the replica set creation, if there are pods created before the replica set creation that match the labels specification of the replica set, then the replica set will also affect pods when creating the replicas
