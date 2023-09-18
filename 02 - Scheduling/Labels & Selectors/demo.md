Note: I already deployed 4 pods and 1 service with differents labels

POD:[env (1xdev and 2xprd) - tier (1xfrontend)]
Service:[env (1xprd)]

1º How many pods exist in the "DEV" environment?

![Alt Text](//00 - images/Scheduling/labels.PNG)


2º How many pods exist in the "PRD" environment?

![Alt Text](//00 - images/Scheduling/labels1.PNG)


3º How many objects are in the "PRD" environment? (including PODS, replicas,services, etc)?

![Alt Text](//00 - images/Scheduling/labels2.PNG)


4º Identify the POD which is part of the "PRD" envinronment and of "FRONTEND" tier ?

![Alt Text](//00 - images/Scheduling/labels3.PNG)


Note: 
As We cans ee in the image below, the selector and the labels from the pod must match.

![Alt Text](//00 - images/Scheduling/labels4.PNG)