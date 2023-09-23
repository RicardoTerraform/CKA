1. **We already delpoyed a pod. The application stores logs at location log/app.log, So view the logs.**

![Alt Text](/00-images/storage/volume2.PNG)

2.  **If the pod was to get deleted now would you be able to view the logs?**

![Alt Text](/00-images/storage/volume3.PNG)
- R: No. So anything that's stored in the log/app.log is stored within the container within the pod. So if the pod gets deleted the logs get deleted as well. As we can see the only volumes that exist is the default volumes.

3. **Configure a volume to store these logs at /home/ubuntu/logs on the host.**

![Alt Text](/00-images/storage/volume.PNG)

![Alt Text](/00-images/storage/volume4.PNG)
- As we can see, the pod is placed in node MASTER so as we are already in the node master we can go to the path /home/ubuntu/logs and we see the app.log... everything is working

4. **Create a Persistent Volume with (Storage: 100Mi - Access: ReadWriteMany - hostPath:/home/ubuntu/)**

![Alt Text](/00-images/storage/volume5.PNG)

5. **Create a Persistent Volume Claim with (Storage: 50Mi - Access: ReadWriteOnce)**

![Alt Text](/00-images/storage/volume6.PNG)

6. **What is the state of the Persistent Volume?**

![Alt Text](/00-images/storage/volume7.PNG)
- R:Available

7. **What is the state of the Persistent Volume Claim?**

![Alt Text](/00-images/storage/volume8.PNG)
- R: Pending

8. **Why is the Claim not bound to the available Persistent Volume?**

![Alt Text](/00-images/storage/volume9.PNG)
- R: The Access Modes MISMATCH. (ex: request properties such as, access modes, volume modes, storage class, etc)

9. **Update the Access Mode on the claim to bind it to the PV**

![Alt Text](/00-images/storage/volume10.PNG)

10. **You request for 50Mi How much capacity is now available to the PVC?**

![Alt Text](/00-images/storage/volume11.PNG)
- R: 100Mi

11. **Update the log pod to use the Persistent Volume Claim as its storage. Replace hostPath configured earlier with the newly created PersistentVolumeClaim**

- on Node worker1 the path /home/ubuntu/pv there is not any file

![Alt Text](/00-images/storage/volume13.PNG)


![Alt Text](/00-images/storage/volume14.PNG)
- The file app.log exist... everything is working well

12. **What is the Reclaim Policy set on the Persistent Volume pv-log?**

![Alt Text](/00-images/storage/volume15.PNG)
- R: Retain

13. **What would happen to the PV if the PVC was destroyed?**

- R: The PV is not deleted but not available

14. **Try deleting the PVC and notice what happen**

![Alt Text](/00-images/storage/volume16.PNG)
- R: the state "deleting" goes forever. it's not get deleted. It's stuck

![Alt Text](/00-images/storage/volume17.PNG)
- R: It is in TERMINATING state because the PVC is being used by a POD

15. **Delete the LOG POD and see what happen with the PVC**

![Alt Text](/00-images/storage/volume18.PNG)
- R: after the pod has been deleted the PVC was deleted too.

16. **What is the state of the PV?**

![Alt Text](/00-images/storage/volume19.PNG)
- R: Released. ler documentação https://kubernetes.io/docs/concepts/storage/persistent-volumes/