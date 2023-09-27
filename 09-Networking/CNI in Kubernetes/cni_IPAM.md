# IP Address Management

- how are the virtual bridge networks in the nodes assigned an IP subnet and how are the pods assigned an IP? 
- Where is this information stored?
- who is responsible for ensuring there are no duplicate IP's assigned?

**CNI Plugin Responsabilities:**
- Must support arguments ADD/DEL/CHECK
- Must support parameters container id, network ns, etc
- Must manage IP address assignment to PODs
- Must return results in a specific format

### how do we manage these IP's?

- CNI comes with 2 built-in plugins to which you can outsource
1. DHCP
2. host-local

- command: cat /etc/cni/net.d/net-script.conf
- in the 'ipam' section we can see the type:'host-local' we can change to dhcp

- Different network solution providers does it differently.
    - ex: weaveworks
    - Weave, by default, allocates the IP range 10.32.0.0/12 for the entire network. That gives the network IP's from range 10.32.0.1 to 10.47.255.254.
    - From this range, the peers decide to split the IP addresses equally between them and assigns one portion to each node. (ex: node1-10.32.0.1; node2-10.38.0.0; node3-10.44.0.0)