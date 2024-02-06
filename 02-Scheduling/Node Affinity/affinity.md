# AFFINITY

Ao utilizarmos "affinity" quando o POD A e o Node A tem a mesma label, automáticamente o POD A vai ser Colocado no NODE A. 

Dois tipos de nodeAffinity:
- requiredDuringSchedulingIgnoredDuringExecution:
	The scheduler vai mandar o pod para o node que tem o mesmo tipo de affinity e caso o pod não consiga encontrar nenhum node com o meu tipo de affinity o mesmo não será colocado
- PreferredDuringSchedulingIgnoredDuringExecution
	Caso o Scheduler não encontre nenhum node com o mesmo tipo de affinity que o pod, ele vai colacar o pod num node que esteja disponível


**How to affinity in pod file:**
```
Spec:
	Container:
		- Name: nginx-app
		Image: nginx 
	affinity:
		nodeAffinity:
			requiredDuringSchedulingIgnoredDuringExecution:
				nodeSelectorTerms:
					- matchExpressions:
						- Key: size
						  Operator: <In> / <NotIn> /<Exists> / etc
						  Values: 
							- Large
```
	
	
- Caso se coloque affinty em algum node e se já existirem pods lá dentro, os mesmo ignorarão as labels e continuarão a correr.
- Caso se coloque affinty em algum node e se existirem pods sem labels esses mesmos pods podem ser colocados nesses nodes com labels

- Com o affinity a única coisa que garante é que se um pod tiver a mesma label que um determiando node ele vai ser automáticamente colocado lá. Mas não garante que outros pods sem label também sejam colocados lá

**COMANDOS:**
```
Kubectl label node <nodename> color=blue
```
