# Storage Class

- It would've been nice if the volume gets provisioned automatically when the application requires it, and that's where storage classes come in.

- With storage classes, you can define a provisioner, such as Google Storage, that can automatically provision storage on Google Cloud and attach that to pods when a claim is made.

- we no longer need the PV definition, because the PV and any associated storage is going to be created automatically when the storage class is created.

-  remember that it still creates a PV, it's just that you don't have to manually create PV anymore. It's created automatically by the storage class.

- There are many other provisioners as well, such as, for AWS EBS, Azure File, Azure Disk, CephFS, Portworx, ScaleIO, and so on.

- So you see, you can create different storage classes, each using different types of disks. For example, a silver storage class with the standard disks, a gold class with SSD drives, and a platinum class with SSD drives and replication. And that's why it's called storage class.

```
storageClass-definition.yaml

apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
    name: google-storage
provisioner: kubernetes.io/gce-pd
```


```
pvc-definition.yaml

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
    name: my-claim
spec:
    accessModes:
        - ReadWriteOnce #ReadOnlyMany#ReadWriteMany
    storageClassName: google-storage
    resource:
        request:
            storage: 500Mi
```

