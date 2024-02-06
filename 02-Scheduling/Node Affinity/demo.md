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
- R: the label color=red is on node sheu

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

### 5. Which nodes can the pods for the red deployment be placed on?
```
#worker node - sheu
kubectl describe node sheu | grep Taint

#Master node - eusebio
kubectl describe node eusebio | grep Taint
```
![Alt Text](/00-images/Scheduling/affinity6.PNG)
- R: In the worker node sheu and in the master eusebio there is no Taint

```
kubectl get pods -o wide
```
![Alt Text](/00-images/Scheduling/affinity11.PNG)
- R: As we can see, the 3 pods from deploy "affinity" are placed in the master and in the worker node(eusebio & sheu)

### 6. Set Node Affinity to the "affinity"" deployment to place the pods on Node SHEU only

- Once I already set up the node SHEU with the label color=red, now I just have to edit the deployment affinity.yaml file.
```
#nano affinity.yaml 
...
spec:
 affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
              - matchExpressions:
                - key: color
                  operator: In
                  values:
                    - red
```
![Alt Text](/00-images/Scheduling/affinity7.PNG)

```
kubectl apply -f affinity.yaml
```
![Alt Text](/00-images/Scheduling/affinity12.PNG)

```
kubectl get pods -o wide
```
![Alt Text](/00-images/Scheduling/affinity13.PNG)
- As we can see now, the 3 pods are placed in the worker node SHEU

### 7. What happen if you remove the label "color=red" from worker node SHEU ?
```
kubectl label node sheu color-
```
![Alt Text](/00-images/Scheduling/affinity14.PNG)

```
#Eliminar o deploy affinity
kubectl delete deploy affinity

#voltar a criar
kubectl apply -f affinity.yaml
```
![Alt Text](/00-images/Scheduling/affinity15.PNG)

```
kubectl get pods -o wide
```
![Alt Text](/00-images/Scheduling/affinity16.PNG)
- R: Verificamos que os pods estão em estado "pending"

```
kubectl describe pod affinity-66b7cff844-krkm7
```
![Alt Text](/00-images/Scheduling/affinity17.PNG)
- R: Vemos que os pods não subiram porque o Affinity color=red que foi definido no pod não encontra nenhum Node com essa label. Sendo assim não é colocado em nenhum NODE fica em estado "pending".
- Tivemos que eliminar o deployment e voltar a criar porque senão apesar dos pods já estarem dentro do Node não ia sortir efeito.



- Conclusão: Se quisermos que um determinado POD seja colocado num Node especifico utilizamos o affinity.