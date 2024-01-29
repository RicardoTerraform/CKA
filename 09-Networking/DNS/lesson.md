# DNS

**How to reach our application?**

http://'service_name'.'namespace'.svc.cluster.local
- that's how services are resolved within the cluster
- curl http://web-service.default.svc.cluster.local

**How to reach our POD?**

- For each pod, Kubernetes generates a name by replacing the dots in the IP address with dashes.
- curl http://10-244-2-5.default.pod.cluster.local


### How to implements DNS?
