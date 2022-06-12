# Automated ELK Stack Deployment
Creating an automated ELK stack deployment process over a network with two web servers.

The files in this repository were used to configure the network depicted below.

![FirstCloud Diagram](https://github.com/kjo024/FirstCloud-Project/blob/main/Diagrams/FirstCloud-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the [install-elk.yml](https://github.com/kjo024/FirstCloud-Project/blob/main/Ansible/install-elk.yml) file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting high traffic connections to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system logs and data.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
|  ELK-VM  |Log Server| 10.1.0.4   | Linux            |
|   Web-1  |Web Server| 10.0.0.5   | Linux            |
|   Web-2  |Web Server| 10.0.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- [Public IP]

Machines within the network can only be accessed by ansible.
- Jump Box: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | [Public IP]          |
| ELK-VM   | No                  | 10.0.0.4             |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because a single playbook can be made to run across multiple machines at once maximizing efficiency.

The playbook implements the following tasks:
- Increase memory usage
- Install docker.io
- Install python3-pip
- Install docker python module
- Install docker container
- Enable docker service

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![sebp.png](https://github.com/kjo024/FirstCloud-Project/blob/main/Images/sebp.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.5
- Web-2: 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat ([playbook](https://github.com/kjo024/FirstCloud-Project/blob/main/Ansible/filebeat-playbook.yml))
- Metricbeat ([playbook](https://github.com/kjo024/FirstCloud-Project/blob/main/Ansible/metricbeat-playbook.yml))

These Beats allow us to collect the following information from each machine:
- Filebeat monitors log data which we can use to monitor activity in the web servers.
- Metricbeat collects metric data which we can use to monitor different metrics such as geo-location, OS type, etc..

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the [install-elk.yml](https://github.com/kjo024/FirstCloud-Project/blob/main/Ansible/install-elk.yml) file to `/etc/ansible/`.
- Update the install-elk.yml file to include the group name 'elk' under hosts
- Run the playbook, and navigate to http://52.183.76.1:5601/app/kibana to check that the installation worked as expected.

![Kibana-Launch.png](https://github.com/kjo024/FirstCloud-Project/blob/main/Images/Kibana-Launch.png)
