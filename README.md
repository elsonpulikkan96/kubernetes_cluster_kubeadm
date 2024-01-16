# kubernetes_cluster_kubeadm
Steps for building a Kubernetes v1.29 Cluster using kubeadm.
bash
Copy code
# control-plane, node-1, and node-2
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.29/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
