# Cluster Upgrade

- Since the kube-apiserver is the primary component in the control plane, and that is the component that all other components talk to, none of the other components should ever be at a version higher than the kube-apiserver. The controller-manager and scheduler can be at one version lower.

kube-apiserver    = v1.10

controller-manager/kube-scheduler = v1.10 ou v1.09

kubelet/kube-proxy = v1.10 ou v1.09 ou v1.08

- The recommended approach is to upgrade one minor version at a time, version 1.10 to 1.11, then 1.11 to 1.12, and then 1.12 to 1.13. The upgrade process depends on how your cluster is set up.

**upgarde cluster**

1. For example, if your cluster is a managed Kubernetes cluster deployed on cloud service providers, like Google, for instance, Google Kubernetes Engine lets you upgrade your cluster easily with just a few clicks. 
2. If you deployed your cluster using tools like kubeadm, then the tool can help you plan and upgrade the cluster. 
3. If you deployed your cluster from scratch, then you manually upgrade the different components of the cluster yourself.

**How it works**
1. o master deve ser atualizado primeiro, mesmo que o amster esteja down não vai impactar os worker nodes, as aplicações vão continuar a trabalhar, caso um pod va abaixo o controller não vai conseguir recriar o pod outra vez uma vez que está em baixo, mas isso pode ser controlar para não impactar serviços de produção a hora de ponta. Não será possível eliminar ou criar novos worloads.

2. depois do master estar atualizado vem o worker nodes. existem diferentes estratégias de upgarde
    1. **todos ao mesmo tempo**: neste sentido a aplicação ficaria em baixo e os users não seriam capazes de utilizar a aplicação. Esta estratégia requer 'DOWNTIME'

    2. **um node de cada vez**: Aqui quando um node vais er atualizado os pods desse node são distribuidos pelos restantes nodes. Quando o 2º node é atualizado acontece o mesmo procedimento, os pods são distribuídos pelo no 1 e 3. quando chega ao 3º node o mesmo procedimento.

    3. **Criação de um node já com a nova versão**: Isto é, temos 3 nodes (exemplo) é criado um node já com a nova versão e um node antigo passa os pods para a nova versão e depois é eliminado, depois de passados os pods, outro node será criado (com a nova versão) e será outra vez passado os pods de um node com versão antiga para o novo node. e assim até ao último node.


### **commands**
- kubectl upgrade plan -> check versions
- apt update
- apt-cache madison kubeadmin -> check what version i want to upgrade

- **upgrade master**
1. kubectl drain master
2. apt-get upgrade -y kubeadmin=1.12.0-00
3. kubeadmin upgrade apply v1.12.0
4. systemctl restart kubelet

- **upgrade worker node - estratégia: um de cada vez**
1. kubectl drain worker1
2. apt-get upgrade -y kubeadmin=1.12.0-00
3. apt-get upgrade -y kubelet=1.12.0-00
4. kubeadmin upgrade node config --kubelet-version v1.12.0
5. systemctl restart kubelet
6. kubectl uncordon worker1

before upgrade we should check the documentation as well