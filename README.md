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
# control-plane, node-1 and node-2
cat << EOF | sudo tee /etc/sysctl.d/99-kubernetes-cri.conf
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
net.bridge.bridge-nf-call-ip6tables = 1
EOF

sudo sysctl --system
```
**Package Installation steps**

```sh
# control-plane, node-1 and node-2
sudo apt update

sudo apt install -y contained
```
Once the packages are installed, generate a default configuration file for containerd on the control plane, node-1 and node-2

```sh
# control-plane, node-1 and node-2
sudo mkdir -p /etc/containerd

sudo containerd config default | sudo tee /etc/containerd/config.toml
```
Change the SystemdCgroup value to true in the containerd configuration file and restart the service

```sh
# control-plane, node-1 and node-2

sudo sed -i 's/SystemdCgroup \= false/SystemdCgroup \= true/g' /etc/containerd/config.toml

sudo systemctl restart containerd
```
We need to install some prerequisite packages on the control plane, node-1 and node-2 for configuring the Kubernetes package repository

```sh
# control-plane, node-1 and node-2

sudo apt update

sudo apt install -y apt-transport-https ca-certificates curl gpg

```
Download the public signing key for Kubernetes package repository on the control plane, node-1 and node-2

```sh
# control-plane, node-1 and node-2

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.29/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```
Add the appropriate Kubernetes apt repository on the control plane, node-1 and node-2
```sh
# control-plane, node-1 and node-2

echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.29/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
Install kubeadm, kubelet and kubectl tools and hold their package version on the control plane, node-1 and node-2

```sh
# control-plane, node-1 and node-2

sudo apt update

sudo apt install -y kubeadm=1.29.0-1.1 kubelet=1.29.0-1.1 kubectl=1.29.0-1.1

sudo apt-mark hold kubeadm kubelet kubectl

```

```sh
# control-plane
sudo kubeadm init --pod-network-cidr 192.168.0.0/16 --kubernetes-version 1.29.0

```
Once the installation is completed, set up our access to the cluster on the control plane

```sh
# control-plane

mkdir -p $HOME/.kube

sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

sudo chown $(id -u):$(id -g) $HOME/.kube/config
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
