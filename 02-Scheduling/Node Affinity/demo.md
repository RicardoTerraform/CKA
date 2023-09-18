1º How many labels exist on worker1 node ?

![Alt Text](/00-images/Scheduling/affinity.PNG)
- 7 labels

2º Apply a label color=red to node worker1

![Alt Text](/00-images/Scheduling/affinity1.PNG)

![Alt Text](/00-images/Scheduling/affinity2.PNG)
- the label color=red is on node worker1

3º Create a deployment named red with 3 replicas.

![Alt Text](/00-images/Scheduling/affinity3.PNG)

![Alt Text](/00-images/Scheduling/affinity5.PNG)
- As we can see a deployment with 3 replicas has been created

4º Which nodes can the pods for the red deployment be placed on?

![Alt Text](/00-images/Scheduling/affinity4.PNG)
- I created another node 'worker2' to be more effective in this demo

![Alt Text](/00-images/Scheduling/affinity6.PNG)
- Any node was Tainted, so the pods can be placed in any node available

5º Set Node Affinity to the red deployment to place the pods on worker1 only

- Once I already set up the node worker1 with the label color=red we just have to edit the deployment file.
![Alt Text](/00-images/Scheduling/affinity7.PNG)
- The image above we can see the 3 pods where placed in each node available, let's place it only on worker1 node.

![Alt Text](/00-images/Scheduling/affinity8.PNG)
- I added some properties in the deployred file, after that I replaced the deployment again(delete and create), and as we can see now the 3 pods are placed in the worker1 node



