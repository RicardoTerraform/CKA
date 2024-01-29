## Manual Scheduling:

- Podemos indicar para qual NODE queremos que o POD seja criado

```
nodeName: node01
```

EX:
```
apiVersion: v1
kind: Pod
metadata:
  labels:
    name: nameimage
spec:
  **nodeName: node01**
  containers:
  - image: nginx:alpine
    name: nameimage
```

- Caso um POD esteja em estado: running não é possível alterar o Node, só se eliminarmos e voltarmos a criar o POD
```
kubectl replace --force -f nginx.yaml
```

- Uma solução também passa pela criação de "Pod-bind-definition.yaml"

EX:
```
apiVersion: v1
kind: Binding
metadata:
  name: nginx
target:
  apiVersion: v1
  kind: Node
  **name: node01**
```
