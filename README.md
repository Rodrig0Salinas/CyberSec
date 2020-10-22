## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/Rodrig0Salinas/Cybersecurity/blob/main/Diagrams/ELK%20Network.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/Rodrig0Salinas/Cybersecurity/tree/main/Ansible

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting overloading the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system logfiles and system services.

The configuration details of each machine may be found below.

|    Name    |  Function  | Private IP Address | Public IP Address | Operating System |
|:----------:|:----------:|:------------------:|:-----------------:|:----------------:|
|   JumpBox  |   Gateway  |      10.0.0.4      |    52.250.12.12   |       Linux      |
|    Web1    | Web Server |      10.0.0.5      |        N/A        |       Linux      |
|    Web2    | Web Server |      10.0.0.6      |        N/A        |       Linux      |
|    Web3    | Web Server |      10.0.0.7      |        N/A        |       Linux      |
|    ELK     | Elk Server |      10.1.0.4      |    40.70.46.68    |       Linux      |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
72.95.27.62

Machines within the network can only be accessed by JumpBox from IP Address 10.0.0.4.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 72.95.27.62 (p22)    |
| Web1     | No                  | 10.0.0.4             |
| Web2     | No                  | 10.0.0.4             |
| Web3     | No                  | 10.0.0.4             |
| ELK      | Yes                 | 72.95.27.62 (p5601)  |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because thanks to it we can make sure all the machines are configured in the same way and that saves us time to focus on other things.

The playbooks implement the following tasks:
* Docker-Install.yml - Downloads and installs Docker as well as DVWA images and configures docker service to be enabled on restart
* ELK-Install.yml - Downloads, installs and configures Elk.
* Filebeat-Install.yml and Metricbeat-Install.yml - Download, install and configure the access for these services.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/Rodrig0Salinas/Cybersecurity/blob/main/Docker%20PS.png


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
* Web1 - 10.0.0.5
* Web2 - 10.0.0.6
* Web3 - 10.0.0.7

We have installed the following Beats on these machines:
* Filebeat. 
* Metricbeat.

These Beats allow us to collect the following information from each machine:
* Filebeat - Collects data from system logs.
* Metricbeat - Collects data from system services.


### Using the Playbooks
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

* Filebeat
SSH into the control node and follow the steps below:
- Copy the configuration file to /etc/ansible/files/.
- Update the configuration file to include your host IP. (Lines 1106 and 1806 - may slightly change)
- Run the Filebeat-Install.yml playbook.

*You can get the configuration file from: https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat

* Metricbeat
SSH into the control node and follow the steps below:
- Run the Metricbeat-Install.yml playbook.

**To execute a playbook you just need to run the command "ansible-playbook" followed by a space and the name of the playbook file**
