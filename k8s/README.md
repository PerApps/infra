# Guide to Kubernetes Essentials

## Overview
Kubernetes, or K8s as it is popularly known, is a powerful open-source platform for managing containerized applications. It automates the deployment, scaling, and management of applications. This guide introduces essential Kubernetes concepts, practical use cases, and actionable tips.

## Table of Contents
1. [Setting Up a Server](#setting-up-a-server)
2. [Configuring the Kubernetes Master](#configuring-the-kubernetes-master)
3. [Adding Workers to the Cluster](#adding-workers-to-the-cluster)

---
## Setting Up a Server
This section provides practical guidance on configuring your server to prepare it for hosting Kubernetes.

### Functionality
When executed, the playbook installs the following key components on your server:
- **Containerd**: v1.7.24
- **Runc**: v1.2.3
- **CNI Plugins**: v1.6.1
- **Kubelet, Kubeadm, and Kubectl**: v1.31.*

These components lay the foundation for your server to function as part of a Kubernetes cluster.

### Location
- For Debian 12: The Ansible playbook is located in the `debian12/setup_server.yaml` directory of this repository.

### Running the Playbook
Follow these steps to run the Ansible playbook for setting up your server:

1. **Prerequisites**:
   - Ensure Ansible is installed and configured on your local machine.
   - Verify that your local machine can communicate with the server via SSH.

2. **Run the Playbook**:
   Execute the following command in your terminal:
   ```bash
   ansible-playbook <os>/setup_server.yaml -i inventory
   ```

---
## Configuring the Kubernetes Master
This section explains how to set up the Kubernetes Master node, which is responsible for managing the cluster.

### Functionality
The playbook installs and configures the following key components:
- **Calico** (v3.29.1): A networking and network security solution for containers, virtual machines, and native host-based workloads. It enhances cluster performance and security.
- **Metrics Server** (v0.7.2): A scalable and efficient source of container resource metrics. It provides insights for resource allocation, automated scaling, and workload management.

### Location
- For Debian 12: The Ansible playbook is located in the `debian12/setup_k8s.yaml` directory of this repository.

### Running the Playbook
Follow these steps to configure the Kubernetes Master:

1. **Prerequisites**:
   - Ensure Ansible is installed and configured on your local machine.
   - Verify SSH connectivity between your local machine and the server.

2. **Install Kubernetes Core Collection**:
   Install the kubernetes.core collection from Ansible Galaxy using the following command:
   ```bash
   ansible-galaxy collection install kubernetes.core
   ```
3. **Run the Playbook**:
   Execute the following command to set up the Kubernetes Master:
   ```bash
   ansible-playbook <os>/setup_k8s.yaml -i inventory
   ```

### Tips
To use `kubectl` on your local machine, you can copy the Kubernetes configuration file from the remote server to your local machine:

1. Copy the configuration file from the remote server:
   ```bash
   scp user@remote-server:/root/.kube/config ~/.kube/config
    ```
---
## Adding Workers to the Cluster
This section explains how to add worker nodes to your Kubernetes cluster.

### Location
- For Debian 12: The Ansible playbook is located in the `debian12/join_k8s.yaml` directory of this repository.

### Running the Playbook
Follow these steps to add workers to your Kubernetes cluster:

1. **Prerequisites**:
   - Ensure Ansible is installed and configured on your local machine.
   - Verify that your local machine can communicate with the server via SSH.

2. **Run the Playbook**:
   Execute the following command to join a worker node to the cluster:
   ```bash
   ansible-playbook <os>/join_k8s.yaml -i inventory
   ```