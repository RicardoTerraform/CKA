# Request & Limits

Request- Nº de cpu ou memória requerida, o node tem que garantir pelo menos aquilo

Limit - é o máximo que o cpu ou a memória que o POD pode consumir

### Comportamentos:

1. NO Request/NO Limits
	- sem request e sem limit um pod pode consumir os recursos todos de CPU de um node e faz com que outro pod não consiga adquirir recursos.
	Não é a melhor prática

2. NO Request/Limits
	- Aqui quando impomos apenas limites, se em cada pod limitarmos o máximo de 3 cpu o que acontece é que aquilo vai só mesmo até ao máximo, caso precisasse de mais 1 cpu já não conseguia.


3. Request/Limits
	- Quando temos o request e o limit se o request for 1 cpu e o limit for 3 estámos a dizer que o node tem que garantir que pelo menos tem 1 cpu e que pode ir até 3 de limit.
	- Normalmente este parece o comportamento mais ideal mas por vezes podemos estar a limitar um pod que até precisa de mais um cpu quando o pod nº2 desse node nem está a precisar. Temos aqui várias perspetivas.


4. Request/NO Limits
	- O cenário ideal seria este. Porquê? Adicionámos o request que faz com que o NODE garanta que aquele pod tem pelo menos aquela quantidade destinada de CPU ou memória. Se tivermos 2 pods apenas com o request ativo ele garante pelo menos aqueles mínimos de CPU e caso o pod nº1 precise de mais CPU pode utilizar sem limitação uma vez que estão livres, e não irá afectar o pod nº2 porque o node garante pelo menos o nº de cpu que foi pedido. E assim se em casos espontâneos algum POD precisar de mais um ou dois cpu que estejam livres não terão essa barreira limitada.


Em conclusão numa vista geral a última opção pode ser a mais aplicada mas lá está depende do objectivo, podem existir situações em que é importante limitar o nº de cpu/memória.


OOMKILLED significa que a memoria crashou, não havia memória suficiente para alocar