# Logging & Monitoring

**Some examples of plataforms to monitor:**
- Metric server
- Prometheus
- Elastic Stack
- DataDog

**comando para verificar cpu e memoria de cada node**
- Kubectl top node
- Kubectl top pod


Install metric server para ser o nosso monitor

O kubelet é que vai guardar esses registos e mandar para o monitor

**COMANDOS**

Verificar logs

#kubectl logs -f pod-name

