1. **Inspect the kubelet service and identify the container runtime endpoint value is set for kubernetes**

- R: ps -aux | grep -i kubelet | grep -i container-runtime

2. **What is the path configured with all binaries od CNI supported plugins?**

- R: cd /opt/cni/bin
- ls

3. **What is the CNI plugin configured to be used on this kubernetes cluster**

- R: ls /etc/cni/net.d

4. **What binary executable file will be run by kubelet after a container and its associated namespace are created?**

- R: cd /etc/cni/net.d
- R: ls
- R: cat <file>
- check the type under the plugins