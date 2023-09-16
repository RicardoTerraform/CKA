# TAINTS & TOLERATIONS

Isto é uma relação entre pod e nodes

Tains: São adicionados aos Nodes

Tolerations: São adicionados aos pods

Exemplo:

Imaginando que temos 3 nodes já criados, de seguida vamos proceder à criação de 5 pods (5), caso não haja restrições(Taints) os 5 pods são criados ao longo dos nodes de forma balanceada. Isto é uma situação normal sem Taints

Vamos agora imaginar o seguinte cenário:
1. Node A está TAINT com uma label=red
2. Node B está TAINT com uma label="blue"
3. Node C está "neutro"(sem taint)

POD A está com uma label=red

POD B está com uma label="blue"

POD C,D,E estão "neutro"(sem toleration)

- O kubernete Scheduler quando for organizar os  criados pelos respetivos Noeds, o POD A ao fazer match com a label do Node A vai pretencer a esse Node (o Node A deixa passar), mas se por exemplo o POD A fosse tentar entrar no Node B, como as labels não fazem match o Node B não iria deixar entrar o POD A.
Referir uma coisa importante, ao utilizarmos taints and toleration não significa que o POD A vai entrar automáticamente no Node A. 
- Exemplo: Apesar de o POD A e o NODE A terem a mesma label não significa que o POD A vai ser inserido automáticamente no NODE A, o POD A também pode ser inserido no NODE C, D ou E. No NODE B não será possível porque ele só deixa entrar se o POD tivesse label=blue, mas como os outros são neutros eles também podem pertencer a esses Nodes.

- Resumindo, Utilizando Taints e Tolerations basicamente só previne que determinados PODs que não tenham a mesma label que o Node não serão inseridos lá, mas não garante que PODS com a mesma label não sejam colocados em Nodes "neutros".  Isto é mais numa de restrições.

## EXISTEM 3 TIPOS DE "TAINT-EFFECT":

- noSchedule: Um pod "neutro" ou um POD que não tenha a mesma Label que o NODE, não irá entrar nesse NODE especifico, irá para outos
- PreferNoSchecule: EX: O scheduler irá tentar evitar colocar o pod "neutro" num NODE com Lebel, mas não é garantido que um Node neutro ou com outra label não vá para esse NODE.
- NoExecute: Novos pods não serão colocados no Node e se já existirem Pods no Node que não tenham as labels serão mandados para fora
	

**How to tolerate in pod file:**

```
Spec:
	Container:
		- Name: nginx-app
		Image: nginx 
	Tolerations:
		- Key: "app"
		Operator: "Equal"
		Value: "blue"
		Effect: "NoSchedule"
```
		

**COMANDOS:**

Remover Taint do NODE
#Kubectl taint node <node-name> "colar aqui o tain-name todo"-node/node-name untainted

Adicionar Taint ao NODE
#Kubectl taint nodes <node-name> key=value:<taint-effect>