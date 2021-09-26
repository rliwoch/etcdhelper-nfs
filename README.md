# Double-tap Enhanced version of etcdhelper

This is a modified version of [etcdhelper](https://github.com/openshift/origin/tree/master/tools/etcdhelper) from OpenShift and a subsequent modifications made by [Flant](https://flant.com/).

One new function in this release: `changeStorageClassNFSServer`

This repo has a new functionality described in the article:

* «**[Hacking Kubernetes etcd for (personal) profit](https://)**».

For the original Flant team article see:
* «**[How to modify etcd data of your Kubernetes directly (without K8s API)](https://blog.flant.com/how-to-modify-etcd-data-of-your-kubernetes-directly-without-k8s-api/)**».

In short, it is designed to change the PV NFS Sever coordinates when using https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner
# Using etcdhelper

## Build

The fastest way is to use official golang image:

```shell
docker run --rm -v $(pwd):/app -w /app -e CGO_ENABLED=0 -e GOOS=linux golang:1.15-alpine go build etcdhelper.go
```

etcdhelper binary will be created in the current directory. Use `GOOS=darwin` to build MacOS executable. 

## Using

### Change NFS Server IP/DNS for a given StorageClass

```shell
./etcdhelper -cacert /etc/kubernetes/pki/etcd/ca.crt -cert /etc/kubernetes/pki/etcd/server.crt -key /etc/kubernetes/pki/etcd/server.key -endpoint https://127.0.0.1:2379 change-storage-class-nfs-server <StorageClassName> <new IP/DNS>
```

# Status

This Double-tap enhanced version of etcdhelper is **PoC (proof of concept)**. Use it on your own risk.
Before making any changes please make sure you BACKUP your `etcd` server.
