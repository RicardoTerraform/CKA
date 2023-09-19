1º A RED deployment has already been deployed. Identify the number of pods deployed by it

![Alt Text](/00-images/lifecycle/update.PNG)

2º Inspect the deployment and identify the current strategy type

![Alt Text](/00-images/lifecycle/update1.PNG)

3º How many PODS can be down for upgrade at a time?

![Alt Text](/00-images/lifecycle/update2.PNG)
- 25% max of pods can be down, so we have 5 pods I would say it goes down 1 pod at each time. In case we have 8 pods It would go down 2 pods at each time 8x25%=2

4º On red deployment change image and describe the changes

![Alt Text](/00-images/lifecycle/update3.PNG)
- image was changed to nginx

![Alt Text](/00-images/lifecycle/update4.PNG)
- As the strategy type is: RollingUpdate, it takes down and up one pod at each time, and we can see that in the events message.

![Alt Text](/00-images/lifecycle/update5.PNG)
- As we learned when a deployment is updated a new replicaset is created

5º Show the history rollouts

![Alt Text](/00-images/lifecycle/update6.PNG)

6º Upgrade to the last version

![Alt Text](/00-images/lifecycle/update7.PNG)
- We can see that before the rollout the replicaset was with 5 pods and after It went to 0. And the previous replicaset was zero and then back to 5. As we learned.

7º Change the strategy type to RECREATE and check the behaviour

![Alt Text](/00-images/lifecycle/update8.PNG)
- As we can see after I changed the image and all pods were taken down and only after that the 5 pods were up


