# Container Network Interface

- Container Runtiome must create network namespace
- Identify network the container must attach to
- Container Runtime to invoke Network Plugin (bridge) when container is ADDed
- Container Runtime to invoke Network Plugin (bridge) when container is DELeted
- JSON format of the Network configuration
- Must manage IP Address assignment to PODs

**Configuring CNI**

- The CNI plugin is configured in the kubelet.Service on each node in the cluster.
- ps -aux | grep kubelet
```
--network-plugin=cni \\
--cni-bin-dir=/opt/cni/bin \\
--cni-conf-dir=/etc/cni/net.d \\
```

- /opt/cni/bin -> has all the supported CNI plugins as executables, such as the bridge, dhcp, flannel, etc

- /etc/cni/net.d -> This is where kubelet looks to find out which plugin needs to be used. If there are multiple files here it will choose the one in alphabetical order.