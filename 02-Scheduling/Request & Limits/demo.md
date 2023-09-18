1º A pod called rabbit is deployed. Identify the Memory requirements set on the pod.

![Alt Text](/00-images/Scheduling/request.PNG)

2º Another pod called rabbit has been deployed. Why it fails?

![Alt Text](/00-images/Scheduling/request1.PNG)
- The pod was not running.

![Alt Text](/00-images/Scheduling/request2.PNG)
- OOM-killed - it is failling because the pod ran out of memory

3º Increase the limit of memory of the rabbit pod to 20Mi

![Alt Text](/00-images/Scheduling/request3.PNG)
- I increased the memory to 20Mi

![Alt Text](/00-images/Scheduling/request4.PNG)
- After the memory has been increased the pod is running now