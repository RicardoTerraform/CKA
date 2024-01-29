# Certified Kubernetes Admin

## Studies and demos

### Raspberry Pi - Kubeadm Cluster on Multiple Nodes

**Install Kubernetes on Ubuntu: Step-by-step process**
1. 2x Raspberry Pi 5 RAW 8GB - Disk 64GB

**Install Kubeadm**

I followed the step-by-step from this link:
https://www.cherryservers.com/blog/install-kubernetes-on-ubuntu#step-9-add-worker-nodes-to-the-cluster


1. Step #1

    sudo swapoff -a

    sudo sed -i '/ swap / s/^/#/' /etc/fstab

    sudo reboot

    After reboot:

    free

    *the swap must be with 0's

    In my case those commands didn´t work, after reboot the swapfile kept showing up, so I did it:

    sudo swapon -s

    sudo systemctl mask swapfile.swap
    
    *if one day I need the swap again I just need to run: sudo systemctl unmask swapfile.swap

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