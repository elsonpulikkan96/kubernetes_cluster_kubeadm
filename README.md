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
sudo hostnamectl set-hostname control-plane

```

```sh
```

