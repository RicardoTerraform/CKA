## DEMO

Note: I already deployed 3 single PODS and 1 Deployment with 2 replicas

```
Pod "red" -> tier=db & env=dev
Pod "blue" -> env=dev
Pod "green -> env=prd
Deploy "grey" -> env=prd 

I used the follow command to create single pods with labels:
kubectl run <pod_name> --image=<image> --labels="env=prd" --dry-run=client -o yaml > grey.yaml
```


1. How many pods exist in the "DEV" environment?
```
kubectl get pods --selector env=dev
```
![Alt Text](/00-images/Scheduling/labels.PNG)


2. How many pods exist in the "PRD" environment?
```
kubectl get pods --selector env=prd
```
![Alt Text](/00-images/Scheduling/labels1.PNG)


3. How many objects are in the "PRD" environment? (including PODS, replicas, services, etc)?
```
kubectl get all --selector env=prd
```
![Alt Text](/00-images/Scheduling/labels2.PNG)


4. Identify the POD which is part of the "DEV" envinronment and of "DB" tier ?
```
kubectl get pods --selector env=dev,tier=db
```
![Alt Text](/00-images/Scheduling/labels3.PNG)


Note: 
As We can see in the image below, the selector and the labels from the pod must match.

![Alt Text](/00-images/Scheduling/labels4.PNG)