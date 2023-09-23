# Volumes

- Docker containers are meant to be transient in nature, which means they are meant to last only for a short period of time. They're called upon when required to process data and destroyed once finished. The same is true for the data within the container. The data is destroyed, along with the container. To persist data processed by the containers, we attach a volume to the containers when they are created. The data processed by the container is now placed in this volume, thereby retaining it permanently. Even if the container is deleted, the data generated or processed by it remains.

```
volume.yaml

apiVersion: v1
kind: Pod
metadata:
    name: volume
spec:
    containers:
        - name: volume-image
          image: nginx
          volumeMounts:
            - mounthPath: /opt
              name: data-volume
    Volumes:
        - name: data-volume
          hostPath:
            path: /data
            type: Directory
```
- com isto se o pod for eliminado nós continuamos com o ficheiro guardado
- it is not recommended for use in a multi node cluster. This is because the pods would use the /data directory on all the nodes, and expect all of them to be the same and have the same data. Since they're on different servers, they're in fact, not the same.
- Unless you configure some kind of external replicated cluster storage solution. Kubernetes supports several types of different storage solutions, such as NFS, cluster affairs, Flocker, fiber channel, Ceph FS, scale io, or public cloud solutions like AWS, EBS, Azure desk, or file, or Google's Persistent Desk.


# Persistent Volumes

- When we created volumes in the previous section, we configured volumes within the pod definition file, so every configuration information required to configure storage for the volume goes within the pod definition file.

- Now, when you have a large environment with a lot of users deploying a lot of pods, the users would have to configure storage every time for each pod. Whatever storage solution is used, the users who deploys the pods would have to configure that on all pod definition files in his environment. Every time there are changes to be made the user would have to make them on all of his pods.

- Instead, you would like to manage storage more centrally. You would like it to be configured in a way that an administrator can create a large pool of storage and then have users carve out pieces from it as required. That is where persistent volumes can help us. A persistent volume is a cluster-wide pool of storage volumes configured by an administrator to be used by users deploying applications on the cluster. The users can now select storage from this pool using persistent volume claims.

```
pv-definition.yaml

apiVersion: v1
kind: PersistentVolume
metadata:
    name: pv-voll
spec:
    accessModes:
        - ReadWriteOnce #ReadOnlyMany#ReadWriteMany
    capacity:
        storage: 1Gi
    hostPath: #this option is not to be used in a production environment.
        path: /tem/data
```

### Commands
- kubectl create -f pv-definition.yaml
- kubectl get pv

# Persistente Volumes Claims

- Persistent Volumes and Persistent Volume Claims are two separate objects in the Kubernetes name space.
- An administrator creates a set of persistent volumes, and a user creates persistent volume claims to use the storage.
- During the binding process, Kubernetes tries to find a Persistent Volume that has sufficient capacity, as requested by the claim.
- And any other request properties such as, access modes, volume modes, storage class, etc
- PVC is a request for a specific amount and type of storage that an application or pod needs. It specifies the storage requirements in terms of capacity and access mode (e.g., ReadWriteOnce, ReadWriteMany, ReadOnlyMany).
- PVCs are used by applications or pods to claim storage resources that match their requirements. If a matching PV is not available, Kubernetes can dynamically provision one based on a defined StorageClass.
- However, if there are multiple possible matches for a single claim, and you would like to specifically use a particular volume, you could still use labels and selectors to bind to the right volumes.
- note that a smaller claim may get bound to a larger volume if all the other criteria matches, and there are no better options. There is a one to one relationship between claims and volumes, so no other claims can utilize the remaining capacity in the volume.
- If there are no volumes available, the persistent volume claim will remain in a pending state until newer volumes are made available to the cluster.

```
pvc-definition.yaml

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
    name: my-claim
spec:
    accessModes:
        - ReadWriteOnce #ReadOnlyMany#ReadWriteMany
    resource:
        request:
            storage: 500Mi
```
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: mypd
  volumes:
    - name: mypd
      persistentVolumeClaim:
        claimName: myclaim
```
POD.yaml

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
    name: my-claim
spec:
    accessModes:
        - ReadWriteOnce #ReadOnlyMany#ReadWriteMany
    resource:
        request:
            storage: 500Mi
```
# PV vs PVC

- In summary, the main difference between PV and PVC is that PV represents a storage resource in the cluster, while PVC is a request for storage by an application or pod. PVs are created and managed independently of applications, while PVCs are created by applications when they need storage resources and are bound to PVs that match their requirements. PVCs are used to abstract the underlying storage details, making it easier to manage storage in a Kubernetes environment.