# kubernetes_cluster_kubeadm

**Introduction**

This guide explains how to set up a three-node Kubernetes v1.29 cluster using kubeadm. Kubernetes is a container orchestration platform, and Kubeadm is a tool used to create and manage Kubernetes clusters.

**What is kubeadm?**

kubeadm is a tool used to create Kubernetes clusters.

It automates the creation of Kubernetes clusters by bootstrapping the control plane, joining the nodes, etc. Follows the Kubernetes release cycle and Open-source tool maintained by the Kubernetes community.

**Prerequisites**

Before setting up the Kubernetes cluster, ensure the following prerequisites are met:

* Create three Ubuntu 22.04 LTS instances for the control plane, node-1, and node-2.

* Each instance must have a minimum specification of 2 CPUs and 2 GB RAM.

* Networking must be enabled between instances.

* Required ports must be allowed between instances.

* Swap must be disabled on instances.

**Steps**


```sh
# control-plane-node
sudo hostnamectl set-hostname control-plane
```

```sh
# node-1
sudo hostnamectl set-hostname node-1
```

```sh
# node-2
sudo hostnamectl set-hostname node-2
```
Update the hosts file on the control plane, node-1 and node-2 to enable communication via hostnames


```sh
# control-plane, node-1 and node-2
sudo vi /etc/hosts
172.31.81.34 control-plane
172.31.81.93 node-1
172.31.90.71 node-2
```
Disable swap on the control plane, node-1 and node-2 and if a swap entry is present in the fstab file then comment out the line

```sh
# control-plane, node-1 and node-2
sudo swapoff -a
sudo vi /etc/fstab
  # comment out swap entry
```
To set containerd as our container runtime on the control plane, node-1 and node-2, first, we need to load some Kernel modules and modify system settings

```sh
# control-plane, node-1 and node-2

cat << EOF | sudo tee /etc/modules-load.d/containerd.conf
overlay
br_netfilter
EOF

sudo modprobe overlay

sudo modprobe br_netfilter
```
```sh

```
```sh

```
```sh

```
```sh

```
```sh

```
```sh

```
```sh

```
```sh

```
```sh

```
```sh

```

