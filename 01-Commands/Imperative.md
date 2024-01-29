## POD

### Create a POD
```
#kubectl run <image-name> --image=<image:version>
```

Generate POD manifest yaml file (will not create)
```
#kubectl run <image-name> --image=<image:version> --dry-run=client -o yaml
```

Create POD with label and labelsvi depl  (filter)
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
#Kubectl taint node node-name "colar aqui o tain-name todo"-node/node-name untainted

Adicionar Taint ao NODE
#Kubectl taint nodes node-name key=value:taint-effect
```
