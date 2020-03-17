# Bigtera VirtualStor CSI

## Overview

This repo contains Bigtera VirtualStor
[CSI](https://github.com/container-storage-interface/)
driver and kubernetes sidecar deployment yamls of provisioner,
attacher, node-driver-registrar and snapshotter for supporting CSI functionalities. Note that this repo is forked from [ceph-csi](https://github.com/ceph/ceph-csi/) project and modified to work with Bigtera VirtualStor only.

## Deployment and Configuration

Bigtera VirtualStor CSI supports both RBD and CephFS backed volumes:

- For details about configuration and deployment of RBD plugin, please refer
  [rbd doc](https://github.com/bigtera-ce/ceph-csi/blob/bigtera-csi/docs/deploy-rbd.md) and
  for CephFS plugin configuration and deployment please
  refer [cephfs doc](https://github.com/bigtera-ce/ceph-csi/blob/bigtera-csi/docs/deploy-cephfs.md).
- For example usage of RBD and CephFS CSI plugins, see examples in `examples/`.

## Supported CO platforms

Bigtera VirtualStor CSI drivers are currently developed and tested **exclusively** on Kubernetes v1.14+ environments.
