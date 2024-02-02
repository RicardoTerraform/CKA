## POD

### Create a POD
```
#kubectl run <image-name> --image=<image:version>
```

Generate POD manifest yaml file (will not create)
```
#kubectl run <image-name> --image=<image:version> --dry-run=client -o yaml
```

Generate POD manifest yaml file (will create)
```
#kubectl run <image-name> --image=<image:version> --dry-run=client -o yaml > red.yaml
```

Create POD with vi depl  (filter)
```
#kubectl run <image-name> --image=<image:version> --labels="tier=db"
#kubectl run <image-name> --image=<image:version> --labels="env=prd","tier=frontend"
```

Create POD with ports
```
#kubectl run <image-name> --image=<image:version> --port=8080
```

Para contar o número de pods podemos utilizar o seguinte comando
```
#Kubectl get pods --no-headers | wc -l
```
### Delete a POD
Eliminar e voltar a criar o mesmo POD
```
#kubectl replace --force -f nginx.yaml
```

Elimnar um POD
```
kubectl delete pod <PODNAME> -n <namespace>
```

Forçar a eliminação de um POD
```
kubectl delete pod <PODNAME> --grace-period=0 --force
```

########################################################################
### DEPLOYMENT
Create a deployment
```
#kubectl create deployment <deploy-name> --image=<image:version> --replicas=3
```

########################################################################
### SERVICES

########################################################################
#### TAINT & TOLERATION
Remover Taint do NODE
```
#Kubectl taint node <node-name> "colar aqui o tain-name todo"-node/node-name untainted
or
#Kubectl taint nodes <node-name> <key=value>:<taint-effect>-

Adicionar Taint ao NODE
#Kubectl taint nodes <node-name> <key=value>:<taint-effect>
```
