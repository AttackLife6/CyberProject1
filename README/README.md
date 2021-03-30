## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://github.com/AttackLife6/CyberProject1/blob/main/README/Images/Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.


 https://github.com/AttackLife6/CyberProject1/blob/main/Ansible/Ansible%20Elk%20Playbook.txt
- Ansible Configuration
- Ansible Filebeat Config file
- Ansible Metricbeat Playbook
- Ansible Metricbeat Config file
- Ansible ELK Installation and VM Configuration
- Ansible Filebeat Playbook

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

Description of the Topology: The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

![image](https://github.com/AttackLife6/CyberProject1/blob/main/README/Images/Topology1.png)
 
![image](https://github.com/AttackLife6/CyberProject1/blob/main/README/Images/ElkTopology.png)

Load balancing ensures that the application will be highly accessable, in addition to restricting traffic to the network.
A Load Balancer on Microsoft Azure protects servers from getting overloaded by traffic and possibly becoming unaccessable. If a single server goes down, the load balancer redirects traffic to the remaining servers automatically. Adding a new server to a server group, the load balancer automatically starts to send requests which improves service availability by preventing downtimes.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

What does Filebeat watch for? Filebeat is a lightweight application installed as an agent on the server to centralize log data. Filebeat monitors log files and locations that users utilize then collects log events and forwards them for logging and indexing. 

What does Metricbeat record? Metricbeat is a lightweight application that when installed it will record and periodically collect data metrics from the server and forwards them for logging and indexing.

The configuration details of each machine may be found below.

|      Name            	|      Function   	|      IP Address 	|      OS      	|
|----------------------	|-----------------	|-----------------	|--------------	|
|     JumpVirtualOne   	|     Gateway     	|     10.0.0.4    	|     Linux    	|
|     VirtualWebOne    	|     Web Server  	|     10.0.0.5    	|     Linux    	|
|     VirtualWebTwo    	|     Web Server  	|     10.0.0.6    	|     Linux    	|
|     ELK-Server       	|     Monitoring  	|     10.1.0.4    	|     Linux    	|


Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpVirtualOne machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Port 5061 which is opened for Kibana

Machines within the network can only be accessed by JumpVirtualOne.
- JumpVirtualOne 10.0.0.4

A summary of the access policies in place can be found in the table below.

|      Name             	|      Publicly Accessible     	|      Allowed IP Addresses     	|      OS      	|
|-----------------------	|------------------------------	|-------------------------------	|--------------	|
|     JumpVirtualOne    	|     Yes                      	|     73.164.27.179             	|     Linux    	|
|     VirtualWebOne     	|     No                       	|     10.0.0.4-254              	|     Linux    	|
|     VirtualWebTwo     	|     No                       	|     10.0.0.4-254              	|     Linux    	|
|     ELK-Server        	|     No                       	|     10.0.0.4-254              	|     Linux    	|



Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- This makes sure it is preventing vulnerabilities.

The playbook implements the following tasks:
- Install docker.io
- Install pip3
- Install Docker python module
- Increase virtual memory
- Download and launch a docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://github.com/AttackLife6/CyberProject1/blob/main/README/Images/DockerPs.png)

Target Machines & Beats

This ELK server is configured to monitor the following machines:
|      Name             	|      Publicly Accessible     	|      Allowed IP Addresses     	|      OS      	|
|-----------------------	|------------------------------	|-------------------------------	|--------------	|
|     VirtualWebOne     	|     No                       	|     10.0.0.4-254              	|     Linux    	|
|     VirtualWebTwo     	|     No                       	|     10.0.0.4-254              	|     Linux    	|

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects data such as log events and sends them to the monitoring cluster these events are typically file system logs.
- Metricbeat collects metrics and statistics about the server and sends them to an output that was specified.


Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to ansible.
- Update the host file to include Web Server and ELK Server.
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.


Which file is the playbook? Where do you copy it? The playbook is ElkPlaybook.yml and can be found in /etc/ansible

Specific commands the user will need to run to download the playbook

- run the command: sudo nano ansible.cfg
- When in the file add the server IP and ansible_python_interpreter=/usr/bin/python3 to the host
- To exit and save use command: Ctrl + x and save the file.
- Make sure you are in the directory that ElkPlaybook.yml is in. 
- run the command: cp ElkPlaybook.yml /etc/ansible
- run the command: sudo nano ElkPlaybook.yml /etc/ansible
- name: installing elk hosts: [your_machine]
- To exit and save use command: Ctrl + x and save the file.
- run the command: ansible-playbook ElkPlaybook.yml
 
