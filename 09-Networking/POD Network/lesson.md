# POD Network

### Networking Model
- Every POD should have an IP address
- Every POD should be able to communicate with every other POD in the same node
- Every POD should be able to communicate with every other POD on other nodes without NAT

**how do you implement a model that solves these requirements?**
-  there are many networking solutions available out there that does these (weaveworks, flannel, cilium, vmware NSX), etc
- let's make ir manually (ex:)

| Nodes    | IP address   |
| -------- | ------------ |
| Node 1   | 192.168.1.11 |
| Node 2   | 192.168.1.12 |
| Node 3   | 192.168.1.13 |

1.  when containers are created, Kubernetes creates network namespaces for them To enable communication between them, we attach these namespaces to a network.

2. Create a bridge network on each node and then bring them up
    - ip link add v-net-0 type bridge
    - ip link set dev v-net-0 up

3. Assign an IP address to the bridge interfaces or networks. Choose any private address range.
    - ip address add 10.244.1.1/24 dev v-net-0
    - ip address add 10.244.2.1/24 dev v-net-0
    - ip address add 10.244.3.1/24 dev v-net-0

    - Now we built our base

4. The remaining steps are to be performed for each container and run every time a new container is created. So I just created a script
    ```
    net-script.sh
    #To attach a container to the network we need a pipe, or virtual network cable.
    #create veth pair
    ip link add ...

    #attach veth pair
    ip link set ...
    ip link set ...

    #assign ip address
    ip -n <namespace> address add ...
    ip -n <namespace> route add ...

    #bring up interface
    ip -n <namespace> link set ...

    ```

    - Now, PODs all get their own unique IP Address on their own nodes

5. The next part is to enable them to reach other Pods on other nodes
    - node1$ ip route add 10.244.2.2 via 192.168.1.12
    - node1$ ip route add 10.244.3.2 via 192.168.1.13

    - node2$ ip route add 10.244.1.2 via 192.168.1.11
    - node2$ ip route add 10.244.3.2 via 192.168.1.13

    - node3$ ip route add 10.244.1.2 via 192.168.1.11
    - node3$ ip route add 10.244.3.2 via 192.168.1.12

- Instead of having to configure routes on each server a better solution is to do that on a router, if you have one in your network, and point all hosts to use that as the default gateway. That way you can easily manage routes to all networks in the routing table on the router.

| Network         | Gateway      |
| --------------- | ------------ |
| 10.244.1.0/24   | 192.168.1.11 |
| 10.244.2.0/24   | 192.168.1.12 |
| 10.244.3.0/24   | 192.168.1.13 |

6. We performed a number of manual steps to get the environment ready with the bridge networks and routing tables. We then wrote a script that can be run for each container that performs the necessary steps required to connect each container to the network, and we executed the script manually. Of course, we don't want to do that, as in large environments where thousands of Pods are created every minute. So how do we run the script automatically when a Pod is created on Kubernetes? That's where CNI comes in, acting as the middleman.

- CNI tells Kubernetes that this is how you should call a script as soon as you create a container.

- modify the script a little bit to meet CNI standards
```
net-script.sh
ADD)
    #create veth pair
    #attach veth pair
    #assign ip address
    #bring up interface
    ip -n <namespace> link set ...

DEL)
    #delete veth pair
```
- The kubelet on each node is responsible for creating containers.
- Whenever a container is created, the kubelet looks at the CNI configuration and identifies our script's name.
    - ex: kubelet.service -> --cni-conf-dir=/etc/cni/net.d
- It then looks in the CNI's bin directory to find our script and then executes the script with the add command and the name and namespace ID of the container.
    - ex: kubelet.service -> --cni-bin-dir=/etc/cni/bin then it execute the script ´net-script.sh add 'container' 'namescpace' 

