é um bom exemplo quando temos um container que queremos adicionar um agente ao pod.
Assim se acrescentarmos mais pods, os dois containers são adicionados e caso haja uma redução de pods os dois containers são removidos automáticamente.

```
apiVersion: v1
kind: Pod
metadata:
    name: nginx
spec:
    containers:
        - name: nginxteste
          image: nginx
        - name: log-agent
          image: log-agent
```