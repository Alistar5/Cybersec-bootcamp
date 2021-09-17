# Cybersec-bootcamp
a collection of work done during cybersecurity bootcamp
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![network with elk server](https://github.com/Alistar5/Cybersec-bootcamp/blob/main/Diagrams/Network%20with%20Elk%20Server.PNG?raw=true)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - [install_elk_playbook.yml](Cybersec-bootcamp/Ansible/install_elk_playbook.yml)
  - [install_filebeat_playbook.yml](Cybersec-bootcamp/Ansible/install_filebeat_playbook.yml)
  - [install_metricbeat_playbook.yml](Cybersec-bootcamp/Ansible/install_metricbeat_playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly adaptible, in addition to restricting connections to the network.
The addition of a load balancer is to protect the availibilty of the web servers. This will help to mitigate downtime in the event of a DDoS attack.
The jump box acts as the gateway to configure the web servers, and allows the web servers to block all traffic except web traffic.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system metrics.
- Filebeat is used to collect data about both web server's file systems.
- Metricbeat records machine metrics about the web servers themselves.

The configuration details of each machine may be found below.

| Name                 | Function       | IP Address | Operating System |   |
|----------------------|----------------|------------|------------------|---|
| Jump-Box-Provisioner | Gateway        | 10.0.0.4   | Linux            |   |
| Elk-Server           | Log Collection | 10.1.0.4   | Linux            |   |
| Web-1                | DVWA hosting   | 10.0.0.5   | Linux            |   |
| Web-2                | DVWA hosting   | 10.0.0.6   | Linux            |   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 193.56.117.90

Machines within the network can only be accessed via SSH into the Jump-Box-Provisioner.
- The Elk server can only be accessed from 193.56.117.90

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses |   |   |
|----------------------|---------------------|----------------------|---|---|
| Jump-Box-Provisioner | Yes                 | 193.56.117.90        |   |   |
| Elk-Server           | Yes                 | 193.56.117.90        |   |   |
| Web-1                | No                  | 193.56.117.90        |   |   |
| Web-2                | No                  | 193.56.117.90        |   |   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Automating the configuration removes much of the room for human error and makes this deployment scalable on a much larger scale.

The playbook implements the following tasks:
- Docker is installed onto the ELK server which is the program used to run and deploy the ELK container.
- The sysctl command is run to increase the virtual memory for this process
- The elk container is downloaded and deployed from a specified image file
- The docker service is also enabled on boot so the container does not need to be manually started.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps](https://github.com/Alistar5/Cybersec-bootcamp/blob/main/images/docker%20ps.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Metricbeat
- Filebeat

These Beats allow us to collect the following information from each machine:
- Metricbeats collects system metrics, which could be used to monitor such things as system uptime. Filebeat collects system logs on the targeted system, logs such as sudo commands used.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk-install.yml file to /etc/ansible.
- Update the hosts file to include the IPs of the machines you wish to install ELK on.
- Run the playbook, and navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana to check that the installation worked as expected.

- install-elk.yml is the playbook file to install ELK, it is copied into /etc/ansible/
- The hosts file in /etc/ansible is edited to select which machines the playbooks are run on, different groups in the host files are used to distuingish which machines get different playbooks.
- Navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana to verify your ELK installation is working.

