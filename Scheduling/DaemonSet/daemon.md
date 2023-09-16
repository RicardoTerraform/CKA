# DaemonSet

DaemonSet é criado automáticamente sempre que um node é criado.

Kube-proxy pode ser criado como um DaemonSet 

DaemonSet pode ser interpretado como um agente, as  log collectors, monitoring agents, or storage daemons.

In summary, DaemonSets in Kubernetes are used to deploy and manage pods across nodes in a cluster, making them useful for running background services and daemons that should be present on all or specific nodes.