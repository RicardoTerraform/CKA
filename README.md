# Certified Kubernetes Admin

## Studies and demos

### Raspberry Pi - Kubeadm Cluster on Multiple Nodes

**Install Kubernetes on Ubuntu: Step-by-step process**
1. 2x Raspberry Pi 5 RAW 8GB - Disk 64GB

**Install Kubeadm**

I followed the step-by-step from this link:
https://www.cherryservers.com/blog/install-kubernetes-on-ubuntu#step-9-add-worker-nodes-to-the-cluster


1. Step #1 Disable swap ON EACH NODE

    ```
    sudo swapoff -a
    sudo sed -i '/ swap / s/^/#/' /etc/fstab
    sudo reboot
    ```
    After reboot:
    ```
    free
    *the swap must be with 0's

    In my case those commands didn´t work, after reboot the swapfile kept showing up, so I did it:
    sudo swapon -s
    sudo systemctl mask swapfile.swap

    *if one day I need the swap again I just need to run: sudo systemctl unmask swapfile.swap
    ```

2. Step #2 Set up the IPV4 bridge ON EACH NODE

    ```
    cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
    overlay
    br_netfilter
    EOF

    sudo modprobe overlay
    sudo modprobe br_netfilter

    # sysctl params required by setup, params persist across reboots
    cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
    net.bridge.bridge-nf-call-iptables  = 1
    net.bridge.bridge-nf-call-ip6tables = 1
    net.ipv4.ip_forward                 = 1
    EOF

    # Apply sysctl params without reboot
    sudo sysctl --system
    ```

3. Step #3 Install kubelet, kubeadm, and kubectl ON EACH NODE

    ```
    sudo apt-get update
    sudo apt-get install -y apt-transport-https ca-certificates curl
    sudo mkdir /etc/apt/keyrings

    curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-archive-keyring.gpg

    echo "deb [signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

    sudo apt-get update

    sudo apt install -y kubelet kubeadm kubectl
    ```

4. Step #4 Install Docker ON EACH NODE

    ```
    sudo apt install docker.io
    sudo mkdir /etc/containerd

    sudo sh -c "containerd config default > /etc/containerd/config.toml"

    sudo sed -i 's/ SystemdCgroup = false/ SystemdCgroup = true/' /etc/containerd/config.toml
    sudo systemctl restart containerd.service
    sudo systemctl restart kubelet.service

    sudo systemctl enable kubelet.service
    ```

5. Step #5 Initialize the Kubernetes cluster on THE MASTER NODE

    ```
    sudo kubeadm config images pull
    sudo kubeadm init --pod-network-cidr=192.168.0.0/16

    * save all information about the token to join other nodes

    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config
    ```

6. Step #6 Configure kubectl and Calico

    I followed this link: https://docs.tigera.io/calico/latest/getting-started/kubernetes/quickstart

    ```
    kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.27.0/manifests/tigera-operator.yaml

    kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.27.0/manifests/custom-resources.yaml
    ```
7. Step #7 Add worker nodes to the cluster

    ```
    * Access the workers node and run the command that was given above:
    kubeadm join 192.168.*.*:6443 --token *********** \
        --discovery-token-ca-cert-hash sha256:853d83e8d5ad**************************
    ```
8. Step #8 Verify the cluster and test

    ```
    *on master node:

    Kubectl get nodes
    Kubectl get pods -A


    * We also need to run the follow command: 
    sudo apt install linux-modules-extra-raspi
    ```

![Alt Text](/00-images/kubeadm/adm1.PNG)

![Alt Text](/00-images/kubeadm/adm2.PNG)