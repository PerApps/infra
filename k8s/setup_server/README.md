# Setting Up Server 
In this repository, you'll find an Ansible playbook dedicated to preparing your server for hosting Kubernetes.

## Location
- For Debian 12:
The Ansible playbook is located in the `debian12/setup` directory of this repository.

## Functionality 
When executed, this playbook will install two key components on your server:
1. **Docker**: A platform that helps you to automate the deployment, scaling, and management of applications using containerization.
2. **Kubeadm**: A tool that provides `kubeadm init` and `kubeadm join` as best-practice "fast paths" for creating Kubernetes clusters.

By doing so, it prepares the groundwork necessary for your server to host Kubernetes successfully.

**Important:** By default, the playbook disables the firewall, ensure your clusters do not require a firewall for production.

## Running the Playbook 
Perform the following steps to run the Ansible playbook for setting up your server:

1. **Prerequisites:** Ensure you have Ansible installed and correctly configured on your local machine. Make sure that your machine can communicate with your server through SSH.

2. **Run the Playbook:** Now you're ready to execute the playbook. Run the following command:
```bash
ansible-playbook debian12/setup.yml -i inventory
```