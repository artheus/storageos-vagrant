# Vagrant StorageOS setup

StorageOS cluster setup with vagrant and Virtualbox on your localhost.

_Note!_ The ansible roles and code is copied from github.com/storageos/deploy

## Pre-requisites

To be able to use this project, you must install some software on
your host first:

* Vagrant
* Virtualbox

## Config

In the upper part of the `Vagrantfile` is the configuration for your
local StorageOS cluster setup.

```
nodes = 3

vmmemory = 2048
vmcpus = 2
```

* `nodes` is the number of nodes to deploy in the cluster
* `vmmemory` is the size of RAM memory for the vm
* `vmcpus` is the number of CPU cores for the vm

## Deploy cluster
```
vagrant up
```

## Destroy cluster
```
vagrant destroy -f
```
