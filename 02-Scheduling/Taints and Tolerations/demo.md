## DEMO

### 1. How many nodes exist on the system?
```
kubectl get nodes
```
![Alt Text](/00-images/Scheduling/taint.PNG)

### 2. Do any Taints exist on worker node "Sheu"?
```
kubectl describe node sheu
```
![Alt Text](/00-images/Scheduling/taint1.PNG)

### 3. Create a Taint on worker node  "Sheu" with key=color, value=red and effect:NoSchedule
```
kubectl taint node sheu color=red:NoSchedule
```
![Alt Text](/00-images/Scheduling/taint2.PNG)

```
kubectl describe node sheu
```
![Alt Text](/00-images/Scheduling/taint3.PNG)

### 4. Create a new pod with pod name mosquito and check what is the state of the pod?
```
kubectl run mosquito --image=nginx
```
![Alt Text](/00-images/Scheduling/taint12.PNG)

```
kubectl run mosquito --image=nginx
```
![Alt Text](/00-images/Scheduling/taint4.PNG)
- State is PENDING

### 5. Why do you think the pod is in a pending state?
```
kubectl describe pod mosquito
```
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