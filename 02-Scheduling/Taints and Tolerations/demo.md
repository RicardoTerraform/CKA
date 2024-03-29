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

### 3. Create a Taint on worker node "Sheu" with key=color, value=red and effect:NoSchedule
```
kubectl taint node sheu color=red:NoSchedule
```
![Alt Text](/00-images/Scheduling/taint2.PNG)

```
kubectl describe node sheu
```
![Alt Text](/00-images/Scheduling/taint3.PNG)

### 4. Create a new POD with pod name mosquito and check what is the state of the POD?
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

### 6. Create a new POD named bee which has a toleration set to the taint COLOR
```
kubectl run bee --image=nginx --dry-run=client -o yaml > templates/bee.yaml

cat templates/bee.yaml
```
![Alt Text](/00-images/Scheduling/taint6.PNG)
- NOTE: we cannot specify toleration in the command line. So let's open our yaml file and add more configurations

```
nano templates/bee.yaml
```

![Alt Text](/00-images/Scheduling/taint7.PNG)

```
cat templates/bee.yaml
```
![Alt Text](/00-images/Scheduling/taint8.PNG)
- NOTE: I edited the POD file (bee.yaml) and now we can see that the POD has a toleration (color=red)

```
kubectl apply -f templates/bee.yaml

kubectl get pods
```
![Alt Text](/00-images/Scheduling/taint9.PNG)
- As the POD bee has the toleration, We can see that the POD bee is running while pod mosquito still pending

### 7. Remove the taint on node worker "Sheu"
```
kubectl taint node sheu color=red:NoSchedule-

kubectl describe node sheu
```

![Alt Text](/00-images/Scheduling/taint10.PNG)
- NOTE: We can see that the Taint on node sheu was removed

```
kubectl get pods
```
![Alt Text](/00-images/Scheduling/taint11.PNG)
- We can see that the pod mosquito is running now, because there is no Taint on worker node "Sheu", even if there are some tolerations in the PODS, It does not matter, the PODS will be scheduled on any available node. Only if there is a Taint on any node, the POD can be scheduled or not, as we saw in this demo so far.