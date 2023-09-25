1. **How many nodes are part of this cluster?**

![Alt Text](/00-images/network/cluster.PNG)
- R: 3

2. **What is the internal Ip address of the Master Node in this cluster?**

![Alt Text](/00-images/network/cluster1.PNG)
- R: 172.29.154.2

3. **What is the network interface configured for cluster connectivity on the Master Node?**

![Alt Text](/00-images/network/cluster2.PNG)
- R: eth0

4. **What is the MAC address of the interface on the Master Node?**

![Alt Text](/00-images/network/cluster3.PNG)
- R: 52:54:00:b0:32:2c

![Alt Text](/00-images/network/cluster4.PNG)
- R: Another option to check it out

5. **What is the  IP address assigned to Worker1 Node in this cluster?**

![Alt Text](/00-images/network/cluster5.PNG)
- R: 172.29.155.101

6. **What is the MAC address of the interface on the Worker1 Node?**

![Alt Text](/00-images/network/cluster6.PNG)
- R: 52:54:00:a9:ea:d5. We must connect the worker1 node, and then execute the command

7. **If you were ping google from the Master Node, which route does it takes? What is the IP address of the Default Gateway?**

![Alt Text](/00-images/network/cluster7.PNG)
- R: 172.29.144.1

8. **What is the port the kube-scheduler is listening on in the controlplane node?**

- R: run the command: netstat -npl | grep -i scheduler

8. **What is the port the etcd is listening on in the controlplane node? And how many client connections established?**

- R: run the command: netstat -npl | grep -i etcd
- R: run the command: netstat -npa | grep -i etcd | grep -i 'port' | wc -l