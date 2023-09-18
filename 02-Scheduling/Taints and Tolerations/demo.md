1º How many nodes exist on the system?

![Alt Text](/00-images/Scheduling/taint.PNG)

2º Do any Tains exist on worker1 node?

![Alt Text](/00-images/Scheduling/taint1.PNG)

3º Create a Taint on worker1 node with key=color, value=red and effect:NoSchedule

![Alt Text](/00-images/Scheduling/taint2.PNG)

![Alt Text](/00-images/Scheduling/taint3.PNG)

4º Create a new pod with pod name mosquito and check what is the state of the pod?

![Alt Text](/00-images/Scheduling/taint4.PNG)
- State is PENDING

5º Why do you think the pod is in a pending state?

![Alt Text](/00-images/Scheduling/taint5.PNG)
- Pod mosquito cannot toletare taint COLOR

6º Create a new pod named bee which has a toleration set to the tain COLOR

![Alt Text](/00-images/Scheduling/taint6.PNG)
- we cannot specify toleration in the command line.

![Alt Text](/00-images/Scheduling/taint7.PNG)

![Alt Text](/00-images/Scheduling/taint8.PNG)
- I edited the pod file and now we can see the pod has a toleration

![Alt Text](/00-images/Scheduling/taint9.PNG)
- As the pod bee has the toleration, We can see the pod bee is running while pod mosquito still pending

7º Remove the taint on node worker1

![Alt Text](/00-images/Scheduling/taint10.PNG)

![Alt Text](/00-images/Scheduling/taint11.PNG)
- We can see the pod mosquito is running now because there is no taint on worker1 node