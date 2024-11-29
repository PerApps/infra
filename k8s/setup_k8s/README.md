# Setting Up the Kubernetes Master
This repository contains an Ansible playbook specifically focused on configuring the Kubernetes node.
This master node serves as the main controlling unit of your Kubernetes cluster, managing its workload, and directing communication across the system.

## Location
- For Debian 12:
The Ansible playbook is located in the `debian12/setup` directory of this repository.

## Functionality
When run, this playbook performs pivotal actions for preparing your server, specifically installing two key components to aid in managing your Kubernetes assets:
1. **Calico:** An open-source networking and network security solution for containers, virtual machines, and native host-based workloads. It helps secure your Kubernetes cluster and enhance its performance.
2. **Metrics Server:** A scalable, efficient source of container resource metrics. These insights facilitate effective resource allocation, automated scaling, and better overall management of your workloads within the Kubernetes cluster.

## Running the Playbook
Execute the Ansible playbook for configuring the Kubernetes by following these steps:

1. **Prerequisites:** Ensure Ansible is installed and correctly configured on your machine. Additionally, verify your machine has successful SSH communication with your server.

2. **Install kubernetes.core:** Before running the playbook, you need to install the `kubernetes.core` collection from Ansible Galaxy. Use the following command to install it:
```bash
ansible-galaxy collection install kubernetes.core
```

3. **Run the Playbook:** With the set preparation, you can now execute the playbook. Enter the following command into your terminal:
```bash
ansible-playbook debian12/setup.yaml -i inventory
```