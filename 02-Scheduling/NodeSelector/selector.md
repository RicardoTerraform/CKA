# Node Selector

- Quando queremos que um pod seja redirecionado para determinado Node, podemos utilizar o NODE_SELECTOR
- Eles identificam-se através das labels, ex: size=Large
- How to label the NODE ?
```
kubectl label nodes <node_name> <label_key>=<lavel_value>
kubectl label nodes sheu size=Large
```
- How to label the POD ?

```
apiVersion:
kind: Pod
metadata: 
    name: myapp-pod
spec:
    containers:
    - name: data-processor
      image: data-processor
    
    **nodeSelector:**
        size: Large
```