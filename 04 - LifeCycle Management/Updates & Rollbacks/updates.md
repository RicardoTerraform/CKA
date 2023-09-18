# UPDATES & ROLLBACKS

### Deployment strategy:
1. Recreate: elimina todos os pods de uma vez e depois de eliminados cria os novos pods com a nova versão (em diferentes replicaset). Obviamente esta não será a melhor estratégia porque no intervalo entre eliminar e criar a aplicação está em baixo.

2. Rolling Update: esta é a estratégia por default. O que isto faz é se tivermos 4 pods. Ele elimina um pod e cria outro pod com a nova versão, só quando o pod nº 1 com a nova versão está criado é que ele volta a eliminar o pod nº2(versão antiga) e cria outro pod com a nova versão e assim sucessivamente. 

- Podemos ver isto no kubectl describe depolyment no atributo "StrategyType"


- UPGRADE: Ao utilizarmos o **Rolling Update**, inicialmente no deployment ele cria um replicaset com os 5 pods(ex:) e quando está a fazer updating ele cria uma nova replicaset com os novos pods da nova versão. se utilizarmos o comando 'kubectl get replicasets' podemos ver as duas criadas, uma com 0 pods (eliminados) e outra já com os 5 pods

- ROLLBACK:
Quando utilizamos o comando 'kubectl undo no rollback', como referi em cima quando ele cria uma nova versão, ele utiliza um replicaset diferente. Então quando ele utiliza o undo ele vai buscar o mesmo replicaset que tinha sido eliminado anteriormente, o replicaset não fica eliminado, o que acontece é que fica com 0 pods.


### Updating image
- Podemos atualizar a imagem do pod diretamente no yaml e depois fazer um kubectl apply
Ou então
- Kubectl set image deployment/my-app name-of-the-docker=nginx1.2.3
- Mas com a última opção devemos ter muito cuidado, porque ao usar isso a nova imagem vai ficar com a versão nova mas as configurações no ficheiro não irão mudar. Mais vale fazer pelo yaml

**COMANDOS**

#kubectl rollout status deployment/my-app

Verificar historico de versões e revisões

#kubectl rollout history deployment/my-app

Voltar para a versão anterior

#kubectl rollout undo deployment/my-app