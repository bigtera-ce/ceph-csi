# Create snapshot

- [Create RBD Snapshot and Clone Volume](#create-rbd-snapshot-and-clone-volume)
  - [Create RBD SnapshotClass](#create-rbd-snapshotclass)
  - [Create RBD Snapshot](#create-rbd-snapshot)
  - [Restore RBD Snapshot to a new PVC](#restore-rbd-snapshot)

**NOTE: At present, there is a limit of 400 snapshots per cephFS filesystem.
Also PVC cannot be deleted if it's having snapshots. Make sure all the snapshots
on the PVC are deleted before you delete the PVC.**

**NOTE: Bigtera VirtualStor CSI Snapshot is currently developed and tested exclusively on Kubernetes v1.19 environments.**

## Create RBD Snapshot and Clone Volume

In the `examples/rbd` directory you will find two files related to snapshots:
[snapshotclass.yaml](../examples/rbd/snapshotclass.yaml)
and [snapshot.yaml](../examples/rbd/snapshot.yaml)

Once you created RBD PVC, you'll need to customize `snapshotclass.yaml` and
make sure the `clusterid` parameter matches `clusterid` mentioned in the
storageclass from which the PVC got created.
If you followed the documentation to create the rbdplugin, you shouldn't
have to edit any other file.

After configuring everything you needed, deploy the snapshotclass:

### Create RBD SnapshotClass

```bash
kubectl create -f snapshotclass.yaml
```

### Verify that the SnapshotClass was created

```console
$ kubectl get volumesnapshotclass
NAME                      AGE
csi-rbdplugin-snapclass   4s
```

### Create RBD Snapshot

```bash
kubectl create -f snapshot.yaml
```

### Verify if your Volume Snapshot has successfully been created

```console
$ kubectl get volumesnapshot
NAME               AGE
rbd-pvc-snapshot   6s
```

### Check the status of the Snapshot

```console
$ kubectl describe volumesnapshot rbd-pvc-snapshot

Name:         rbd-pvc-snapshot
Namespace:    default
Labels:       <none>
Annotations:  <none>
API Version:  snapshot.storage.k8s.io/v1alpha1
Kind:         VolumeSnapshot
Metadata:
  Creation Timestamp:  2019-02-06T08:52:34Z
  Finalizers:
    snapshot.storage.kubernetes.io/volumesnapshot-protection
  Generation:        5
  Resource Version:  84239
  Self Link:         /apis/snapshot.storage.k8s.io/v1alpha1/namespaces/default/volumesnapshots/rbd-pvc-snapshot
  UID:               8b9b5740-29ec-11e9-8e0f-b8ca3aad030b
Spec:
  Snapshot Class Name:    csi-rbdplugin-snapclass
  Snapshot Content Name:  snapcontent-8b9b5740-29ec-11e9-8e0f-b8ca3aad030b
  Source:
    API Group:  <nil>
    Kind:       PersistentVolumeClaim
    Name:       rbd-pvc
Status:
  Creation Time:  2019-02-06T08:52:34Z
  Ready To Use:   true
  Restore Size:   1Gi
Events:           <none>
```

### Restore RBD Snapshot

To restore the snapshot to a new PVC, create
[pvc-restore.yaml](../examples/rbd/pvc-restore.yaml)
and a testing pod [pod-restore.yaml](../examples/rbd/pod-restore.yaml)

```bash
kubectl create -f pvc-restore.yaml
kubectl create -f pod-restore.yaml
```

