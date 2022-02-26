# Cloud Network
This is a collection of Linux Scripts and Ansible Scripts from my George Washington University Cybersecurity Class.

Most of the scripts are used to configure cloud servers with differnt docker containers.

The final setup was for servers running vulnerable DVWA containers along with a jump box and a server running an ELK stack container.


## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Images/My Diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ANSIBLE file may be used to install only certain pieces of it, such as Filebeat.

filebeat-playbook.yml
filebeat-config.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly AVAILABLE, in addition to restricting ATTACKS to the network.
ONLY THE JUMPBOX CAN ACCESS VMS, LIMITING OPPOTUNITY FOR ATTACKS.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the LOGS and system TRAFFIC.
FILEBEAT MONITORS LOG FILES< COLLECTS LOG EVENTS AND FORWARDS THEM
METRICBEAT MONITORS YOUR SYSTEM AND THE PROCESSES RUNNING

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  |10.0.0.4    |Linux             |
| WEB-1    | Server   |10.0.0.5    |Linux             |
| Web-2    | Server   |10.0.0.7    |Linux             |
| web-3    | Server   | 10.0.0.8   |Linux             |
| elkvm    | Monitor  |10.1.0.4    |Linux             |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JUMPBOX machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
WHITELISTED IP ADDRESSES ARE:

5061 KIBANA PORT
138.88.227.223 - my personal IP
23.100.24.61 - my JUMPBOX IP

Machines within the network can only be accessed by JUMPBOX
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
	ELKVM public IP 40.69.124.15 with port 5061

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 23.100.24.61         |
| web-1    | no                  |  10.0.0.5            |
| web-2    | no                  |  10.0.0.7            |
| web-3    | no                  | 10.0.0.8             |
|elkvm     |no                   |10.1.0.4              |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
allowed to watch out for easily overlooked vulnerabilityies. It was easier to look at the configuration as a whole

The playbook implements the following tasks:
-Install docker.io
-Install python3-pip
-Increase memory use
-download elk container
-laucher and start elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Images/sudo docker ps.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
web-1 10.0.0.5
web-2 10.0.0.7
web-3 10.0.0.8

We have installed the following Beats on these machines:
Filebeat
METRIC BEAT

These Beats allow us to collect the following information from each machine:
FILEBEAT COLLECTS LOG DATE AND DISPLAYS IN MONITORING. METRICBEAT COLLECTS STATS AND SHOWS IN OUTPUT AS ELASTICSEARCH OR LOGSTASH

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook.yml file to Ansible.
- Update the host file to include webservers(IP) and ELK
- Run the playbook, and navigate to KIBANA to check that the installation worked as expected.
- 40.69.124.15:5061/app/kibana


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

ansible-playbook /etc/ansible/roles/filebeat-playbook.yml
nano /etc/ansible/hosts
