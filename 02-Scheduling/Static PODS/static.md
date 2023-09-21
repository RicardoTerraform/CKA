# Static PODS

- Podemos configurar um kubelet sem ter o kube-apiserver.
- Podemos criar um kubelet para ler os pods desde a diretoria seguinte: /etc/kubernetes/manifest
- Esses pods que são gerados sem intervenção do kube-apiserver são chamadados de static pods
- Não é possível criar réplicas, deployments ou mesmo serviços (porque estes componentes tem outras arquiteturas por detrás)
- Kubelet apenas understand pod
- Para verificar se um pod é static podemos listar todos os pods e Todos os pods que terminarem com o mesmo nome que o node significa que é static.
- Outra forma, É abrir o describe do objecto e onde diz "ownerReference" verificar se o KIND é "node"


**Onde é que podemos configurar aquela diretoria?**
1. podemos aceder aos kubelet.service
 - onde tem "--.pod-manifest-path=/etc/kubernetes/manifest 
 - e podemos alterar para outra diretoria

2. podemos aceder ao kubelet do node
 - Posso aceder a um node através do Internal IP: ssh 10.38.2.67
 - kubelet/config.yaml
 - StaticPodPath: /etc/kubernetes/manifest 

