POD
Create a POD
#kubectl run <image-name> --image=<image:version>

Generate POD manifest yaml file (will not create)
#kubectl run <image-name> --image=<image:version> --dry-run=client -o yaml

Create POD with label and labelsvi depl  (filter)
#kubectl run <image-name> --image=<image:version> --labels="tier=db"
#kubectl run <image-name> --image=<image:version> --labels="env=prd","tier=frontend"

Create POD with ports
#kubectl run <image-name> --image=<image:version> --port=8080

Para contar o número de pods podemos utilizar o seguinte comando
#Kubectl get pods --no-headers | wc -l


DEPLOYMENT
SERVICES

