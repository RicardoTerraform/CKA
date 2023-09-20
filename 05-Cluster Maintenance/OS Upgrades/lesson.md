# OS UPGRADE


- So you have a cluster with a few nodes and pods serving applications. What happens when one of these nodes go down? Of course, the pods on them are not accessible. Now depending upon how you deployed those pods, your users may be impacted.

- For example, if we have multiple replicas of the blue pod, and if one node goes down the users accessing the blue application are not impacted as they are being served through the other blue pod that's online. However, users accessing the green pod (just have one pod in that node) are impacted as that was the only pod running the green application.

- Now, what does Kubernetes do in this case? If the node came back online immediately, then the kubelet process starts and the pods come back online. However, if the node was down for more than five minutes, then the pods are terminated from that node.
    - by default the node can be down for 5min
    - kube-controller-manager --pod-eviction-timeout=5m0s

- So whenever a node goes offline, the master node waits for up to five minutes before considering the node dead. When the node comes back online after the pod-eviction-timeout, it comes up blank without any pod scheduled on it. Since the blue pod was part of a replica set, it had a new pod created on another node. However, since the green pod was not part of a replica set, it's just gone.

- se precisarmos de fazer alguma manutenção no node e sabemos que vai estar pronto dentro de 5minutos é ok, mas se soubermos que vai se rmais demorado, mais do que 5 minutos podemos usar alguns comandos. Nós podemos 'drain the node' 
    - kubectl drain node-1

- com este comando é criado os pods são recreados num node já existente. e o node é amrcado como 'corned' or como 'unschedulable'

- Quando o node já estiver ok, ele volta online mas vazio, então temos que remover a situação e usámos o seguinte comando:
    - kubectl uncordon node-1

- Também podemos usar um comando de forma a que nenhum  new pod seja marcado para interar esse NODE
    - kubectl cordon node-2


### comandos
1. kubectl drain node-1 -> passa os pods para outro node e fica unschedulable
2. kubectl uncordon node-1 -> remove o drain
3. kubectl cordon node-2 -> fica indisponível para que novos pods não sejam inseridos lá






