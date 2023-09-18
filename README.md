# Certified Kubernetes Admin

## Studies and demos

### Multipass Microk8s Cluster on Multiple Nodes

**Create the vms**
1. multipass launch -n master -m 2G -c 2 -d 4G
2. multipass launch -n worker1 -m 2G -c 2 -d 4G
3. multipass list

![Alt Text](/00-images/microk8s/micro.PNG)

**Install microk8s master node**

To create the master I will install microk8s and get some basic configuration and modules up and running.

1. multipass shell master
2. sudo snap install microk8s --classic
3. sudo usermod -a -G microk8s $USER
4. sudo chown -f -R $USER ~/.kube
5. exit
6. Multipass restart master
7. multipass shell master
8. microk8s status --wait-ready
9. echo "alias kubectl='microk8s kubectl'" >> ~/.bash_aliases
10. source ~/.bash_aliases
11. microk8s enable dns storage
12. sudo microk8s add-node
- save this information

**Install microk8s worker1 node**

Join the nodes to the cluster 

1. multipass shell worker1
2. sudo snap install microk8s --classic
3. sudo microk8s join 172.27.97.226:25000/65cb5c78f450b329dae84b78a60fd097/26fcb251c28d
4. exit

**Check it out if everything is working properly**

1. multipass shell master
2. microk8s kubectl get nodes

![Alt Text](/00-images/microk8s/micro1.PNG)