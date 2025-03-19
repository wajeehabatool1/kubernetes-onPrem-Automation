# kubernetes-onPrem-Automation
---------------------------------------------
## Overview
This repository provides an automated approach to deploying a Highly Available (HA) Kubernetes cluster using Kubeadm with a stacked etcd topology. The setup consists of multiple control planes, worker nodes, and HAProxy load balancers, ensuring fault tolerance and high availability.

The automation leverages Ansible and Vagrant to efficiently provision and configure the Kubernetes cluster. Additionally, Keepalived is used alongside HAProxy to ensure redundant and highly available load balancers, preventing a single point of failure.

This setup is flexible—you can add or remove control planes and worker nodes as needed while maintaining quorum for etcd and distributing traffic efficiently.

-----
## System Requirements
### Minimum Hardware Requirements:
- **Control Plane Node** : At least 3 nodes (can be more, must maintain quorum) with 4GB RAM, 2 vCPUs each
- **Worker Node**:At least 1 node  with 4GB RAM, 2 vCPUs each
- **Load Balancers**: At least 2 nodes (can be more for HA) with 2GB RAM, 1 vCPU each
### Software Requirements:
- Vagrant (for VM provisioning)
- Ansible (for automation)
----
## Deployment Steps
### 1.Clone the Repository
  ``` bash 
    git clone https://github.com/wajeehabatool1/kubernetes-onPrem-Automation.git
    cd kubernetes-onPrem-Automation
   ```
### 2.Initialize Vagrant Environment
   Navigate to the Vagrant folder and start the virtual machines:
  ``` bash
     cd vagrant
    vagrant up
  ```

### 3.Configure the Cluster Using Ansible 
   Once the VMs are up, navigate to the Ansible directory and run the playbook:
  ``` bash
    cd ../ansible
    ansible-playbook main.yml -i inventory/inventory.ini -vvv
  ```
  - Add -v, -vv, or -vvv for verbose output

### 4. Verify the Cluster
 -  Mnaually ssh into any controlplane node such as 
 ``` bash
     vagrant ssh controlplane1
 ```
 -  escalate privileges to the root user
    ``` bash
    sudo -i
    ```
 -  run the below command to verify all nodes are up
    ``` bash
    kubectl get nodes
    ```
---------------------------

For a detailed manual setup of a highly available Kubernetes cluster using a stacked etcd topology and HAProxy, you can refer to another project:[HA-K8s-Cluster-Stacked-etcd-HAProxy](https://github.com/wajeehabatool1/HA-K8s-Cluster-Stacked-etcd-HAProx). This resource provides insights into manual configurations and complements the automated approach presented in this repository.

---------------------------
## Contribution
We welcome contributions! If you would like to improve or extend this project, please review the [Contributor Guidelines](https://github.com/wajeehabatool1/kubernetes-onPrem-Automation/blob/main/Contributions.md) before submitting a pull request.

----------------------
## License
This project is licensed under the MIT License.

----------------------

  

