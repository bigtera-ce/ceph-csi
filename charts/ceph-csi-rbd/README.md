# ceph-csi-rbd

The ceph-csi-rbd chart adds rbd volume support to your cluster.

## Install Chart

Optionally, create a kubernetes namespace, say "ceph-csi-rbd", if you don't want mess up existing one.

```bash
kubectl create namespace ceph-csi-rbd
```

To install the Chart into the namespace "ceph-csi-rbd" of your Kubernetes cluster

```bash
helm install --namespace "ceph-csi-rbd" ceph-csi-rbd charts/ceph-csi-rbd
```

After installation succeeds, you can get a status of Chart

```bash
helm status --namespace "ceph-csi-rbd" ceph-csi-rbd
```

If you want to delete your Chart, use this command

```bash
helm delete --namespace "ceph-csi-rbd" ceph-csi-rbd
```

If you want to delete the namespace, use this command

```bash
kubectl delete namespace ceph-csi-rbd
```
