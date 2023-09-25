# Cluster Networking

### Master Nodes
| Protocol | Port Range   | Purpose                 | Used by              |
| -------- | ------------ | ----------------------- | ---------------------|
| TCP      | 6443         | Kubernetes API Server   | All                  |
| TCP      | 2379-2380    | etcd server client API  | kube-apiserver, etcd |
| TCP      | 10250        | kubelet API             | self, control plane  |
| TCP      | 10259        | kube-scheduler          | self                 |
| TCP      | 10257        | kube-controller-manager | self                 |

### Worker Nodes
| Protocol | Port Range   | Purpose                 | Used by              |
| -------- | ------------ | ----------------------- | ---------------------|
| TCP      | 10250        | Kubelet API             | self, control plane  |
| TCP      | 30000-32767  | etcd server client API  | All                  |


