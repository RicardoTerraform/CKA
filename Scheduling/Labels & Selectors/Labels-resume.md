LABELS:
Labels Funcionam como filtros
	Ex: kubectl get pods --selector env=dev
	Ou
	kubectl get pods --selector env=dev, tier=frontend, bu=finance


SELECTORS:
Selectors são usados para fazermos a ligação dos pods com deployments ou principalmente com os serviços.

No selector: 
    matchLabels: devemos utilizar as labels utilizadas no POD para garantirmos que esse pod pertence mesmo a esse deployment ou serviço

    Annotations: São utilziados para guardar outros detalhes para outro tipo de informações
	    Por examplo: Detalhes de tools, versões ou detalhes de contactos, telefone, emails, ids etc que podem ser utilizados para algum tipo de integrações
		
