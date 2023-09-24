1. **How many StorageClass exist in the cluster right now?**

![Alt Text](/00-images/storage/class.PNG)

2. **What is the name of the StorageClass thar does not support dynamic volume provisioner?**

![Alt Text](/00-images/storage/class2.PNG)
- R: delayed-volume-sc.  we know that the provisionary is what defines how the storage class volumes are provisioned. So the no provisioner is one that does not support dynamic volume provisioning.

3. **What is the Volume Binding Mode used for that storage class?**

![Alt Text](/00-images/storage/class1.PNG)
- R: WaitForFirstConsumer

4. **Is there a PersistentVolumeClaim that is consuming the PersistentVolume called pv-log?**

![Alt Text](/00-images/storage/class3.PNG)
- R: No

5. **Create a new PVC by the name of local-pvc that should bind to the volume pv-log**

![Alt Text](/00-images/storage/class4.PNG)
- R: It's created

![Alt Text](/00-images/storage/class5.PNG)
- R: It's in Pending state, because it's waiting for the first consumer to be created

- So the StorageClass called delayed-volume-sc makes use of VolumeBindingMode set to WaitForFirstConsumer. So this will delay the binding and provisioning of PersistenVolume until a pod using the PersistentVolumeClaim is created.

6. **Create a new pod called nginx with the image nginx:alpine. The Pod should make use of the PVC local-pvc and mount the volume ate the path /var/www/html. The PV local-pv should in a bound state**

![Alt Text](/00-images/storage/class6.PNG)
- R: Pod is created. But It is in Pending state. Let's fix it.

![Alt Text](/00-images/storage/class7.PNG)
- R: The Access Mode mismatch. let's fix it

![Alt Text](/00-images/storage/class8.PNG)
- R: After all changes. The pod is running

7. **What is the status of the local-pvc PVC now?**

![Alt Text](/00-images/storage/class9.PNG)
- R: Bound. It's working as expect

![Alt Text](/00-images/storage/class10.PNG)
- R: Now the PV as a claim associated

8. **Create a new StorageClass where the VolumeBindingMode is Immediate**

![Alt Text](/00-images/storage/class11.PNG)
- R: As we can see once the VolumeBindingMode is Immediate, after creating a pv and a pvc the PVC gets immediate associated with the PV, and the status is Bound.

- We created a PV file because the storage class is no-provisioner. Otherwise the storageclass would have created the PV automatically.
