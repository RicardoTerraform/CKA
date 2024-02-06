## DEMO

### 1. How many labels exist on node SHEU ?
```
kubectl describe node sheu
```
![Alt Text](/00-images/Scheduling/affinity.PNG)
- R: 5 labels

### 2. What is the value set to the label "beta.kubernetes.io/arch" on node SHEU
```
kubectl describe node sheu
```
![Alt Text](/00-images/Scheduling/affinity9.PNG)
- R: arm64


### 3. Apply a label color=red to node SHEU
```
kubectl label node sheu color=red
```
![Alt Text](/00-images/Scheduling/affinity1.PNG)

```
kubectl describe node sheu
```
![Alt Text](/00-images/Scheduling/affinity2.PNG)
- the label color=red is on node sheu

### 4. Create a deployment named "affinity" with 3 replicas.
```
#only output
kubectl create deployment affinity --image=nginx --replicas=3 --dry-run=client -o yaml

kubectl create deployment affinity --image=nginx --replicas=3 --dry-run=client -o yaml > affinity.yaml
```
![Alt Text](/00-images/Scheduling/affinity3.PNG)

```
kubectl apply -f affinity.yaml
```
![Alt Text](/00-images/Scheduling/affinity5.PNG)
- As we can see a deployment with 3 replicas has been created

```
kubectl get deploy

kubectl get pods
```
![Alt Text](/00-images/Scheduling/affinity10.PNG)

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



