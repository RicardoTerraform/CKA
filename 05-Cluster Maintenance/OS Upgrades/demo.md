1º how many nodes do you see in the cluster?

![Alt Text](/00-images/clusterMaintenance/upgrade.PNG)

2º how many applications do you see hosted on the cluster?

![Alt Text](/00-images/clusterMaintenance/upgrade1.PNG)

3º which nodes are the application hosted on ?

![Alt Text](/00-images/clusterMaintenance/upgrade2.PNG)
- master, worker1 and worker2

4º We need to take node Worker2 out for maintence. Empty the node of all applications and mark it unshedulable.

![Alt Text](/00-images/clusterMaintenance/upgrade3.PNG)

![Alt Text](/00-images/clusterMaintenance/upgrade5.PNG)

5º what nodes are the apps on now?

![Alt Text](/00-images/clusterMaintenance/upgrade4.PNG)
- after drained the node worker2, the pods where replaced in different nodes, master and worker1

6º Configure the node Worker2 to be schedulable again

![Alt Text](/00-images/clusterMaintenance/upgrade6.PNG)

7º how many pods are scheduled on node Worker2 now ?

![Alt Text](/00-images/clusterMaintenance/upgrade7.PNG)
- NONE

8º why are there no pods on node Worker2 ?
- only when new pods are created they will be scheduled

9º create a pod in node Worker2 and try to drain it again.

![Alt Text](/00-images/clusterMaintenance/upgrade8.PNG)
- An orange pod was created in Node Worker2, as we can see

![Alt Text](/00-images/clusterMaintenance/upgrade9.PNG)
- there is an error because there is a single pod (orange pod) in node worker2 which is not part of a replicaset, it means that if a force to drain the node the orange pod will be deleted forever because its not a deployment or replicaset.

10º If we have a critical application and we do not want it to be removed and we do not want to shedule any more pods on node worker2

![Alt Text](/00-images/clusterMaintenance/upgrade10.PNG)
- if the node is 'cordon' no more pods will be placed in this node

