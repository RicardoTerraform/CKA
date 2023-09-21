# Backups and Restore

### Backup Candidates
1. Resource Configuration
2. ETCD Cluster
3. Persistent Volumes


### Resource Configuration

**Imperative**

- What if someone created an object the imperative way without documenting that information anywhere? So a better approach to backing up resource configuration is to query the Kube API server. Query the Kube API server using the kubectl, or by accessing the API server directly, and save all resource configurations for all objects created on the cluster as a copy. 
- For example, one of the commands that can be used in a backup script is to get all pods, and deployments, and services in all namespaces using the kubectl utility's get all command, and extract the output in a YAML format, then save that file. And that's just for a few resource group. There are many other resource groups that must be considered. Of course, you don't have to develop that solution yourself. There are tools like Ark, or now called Velero, by Heptio, that can do this for you. It can help in taking backups of your Kubernetes cluster using the Kubernetes API.

**Declarative**

- This is the preferred approach if you want to save your configuration, because now, you have all the objects required for a single application in the form of object definition files in a single folder. This can easily be reused at a later time, or shared with others. Of course, you must have a copy of these files saved at all times. 
- A good practice is to store these on source code repositories, that way it can be maintained by a team. The source code repository should be configured with the right backup solutions. With managed or public source code repositories like GitHub, you don't have to worry about this. With that, even when you lose your entire cluster, you can redeploy your application on the cluster by simply applying these configuration files on them.

### ETCD

- The etcd cluster stores information about the state of our cluster.
- etcd cluster is hosted on the master nodes.
- in the file etcd.service, in the propertie --data-dir=/var/lib/etcd , we can specified a location where all the data would be stored. That is the directory that can be configured to be backed up by your backup tool.
- we can take a snapshot of the etcd database
**backup**
```
kubectl describe pods (etcd-name) -n kubesystem
#get all informations
or
kubectl describe pods (kube-apiserve-name) -n kubesystem
#--etcd-server podemos validar se é static(127.x.x) ou external(192.x.x.)

ETCDCTL_API=3 etcdl \
    snapshot save snapshot-pre-boot.db --endpoint=... \
    --cacert= (location) \
    --cert= (location) \
    --key= (location) \
    /(location where I want to store de db)
```
- when you're taking a snapshot, you're actually taking a snapshot by contacting the etcd server directly. And by, and for that you need all the certificates.
```
ETCDCTL_API=3 etcdl \
    snapshot status snapshot.db
```
**Restore backup - ETCD**
1. service kube-apiserver stop
2. 
```
ETCDCTL_API=3 etcdl \
    snapshot restore \
    --data-dir (location where we want the backup to be restored too and the location of the file)
    ex: --data-dir /var/lib/etcd-from-backup /var/opt/snapshot-pre-boot.db
```
```
ls /var/lib/etcd-from-backup
only to check if the backup is there
```

- analisar etcd yaml, analisar o volume e validar/alterar para a nova diretoria
- ou então apenas alterar a diretoria --data-dir para a nova

3. systemctl daemono-reload
4. service etcd restart
5. service kube-apiserver start
