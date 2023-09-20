1º Check if the GREEN POD has any InitContainer

![Alt Text](/00-images/lifecycle/init.PNG)
- there is one InitContainer

2º Check the status of YELLOW POD

![Alt Text](/00-images/lifecycle/init1.PNG)
- the status is pending because we are running an initcontainer that takes 60s. That's why the pod is pending. Let's check the status after 60s (below image)

![Alt Text](/00-images/lifecycle/init2.PNG)
- As we can see the status is running now

3º A new application orange is deployed. There is something wrong with it. Identify and fix it

![Alt Text](/00-images/lifecycle/init3.PNG)
- we can see, there is an error

![Alt Text](/00-images/lifecycle/init4.PNG)
- in the event logs we see that there is a WARNNING.. initcontainer is always restarting. Let's check the logs

![Alt Text](/00-images/lifecycle/init5.PNG)
- the container logs says it's waiting to start: PodInit, so than we check the logs only to the initContainer. We can see that the command sleep is wrong. there is an error in the command. Let's fix the error and see what's happen.

![Alt Text](/00-images/lifecycle/init6.PNG)
- After fix the command the pod is running now

