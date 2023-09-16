How to affinity in pod file:
…..
Spec:
	Container:
		- Name: nginx-app
		Image: nginx 
	Affinity:
		nodeAffinity:
			requiredDuringSchedulingIgnoredDuringExecution:
				nodeSelectorTerms:
					- matchExpressions:
						- Key: size
						  Operator: In
						  Values: 
							- Large
						
						
						
						
Dois tipos de nodeAffinity:
-requiredDuringSchedulingIgnoredDuringExecution:
	The scheduler vai mandar o pod para o node que tem o mesmo tipo de affinity e caso o pod não consiga encontrar nenhum node com o meu tipo de affinity o mesmo não será colocado
-PreferredDuringSchedulingIgnoredDuringExecution
	Caso o Scheduler não encontre nenhum node com o mesmo tipo de affinity que o pod, ele vai colacar o pod num node que esteja disponível
	
	
Caso se coloque affinty em algum node e se já existirem pods lá dentro, os mesmo ignorarão as labels e continuarão a correr
Caso se coloque affinty em algum node e se existirem pods sem labels esses mesmos pods podem ser colocados nesses nodes com labels

Com o affinity a única coisa que garantem é que se um pod tiver a mesma label que um node ele vai ser automáticamente colocado lá. Mas não garabnte que outros pods sem label também sejam colocados lá


Kubectl label node nodename color=blue