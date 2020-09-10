## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/elk_stack_diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. 
They can be used to recreate the entire deployment pictured above. 
Alternatively, select portions of an Ansible playbook file, like filebeat-playbook.yml, 
may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly stable and resiliant against DDoS attacks, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system metrics.


The configuration details of each machine may be found below.

|Name     |Function         |IP Address |Operating System |
|---------|-----------------|-----------|-----------------|
|Jump-Box |Gateway          |10.0.0.4   |Ubuntu           |
|Web-1    |Web/DVWA Server  |10.0.0.5   |Ubuntu           |
|Web-2    |Web/DVWA Server  |10.0.0.6   |Ubuntu           |
|ELK4444  |ELK Stack Server |10.1.0.4   |Ubuntu           |


### Access Policies

Not all of the virtual machines of the internal network are exposed to the public Internet. 

Only the Jump-Box and the ELK4444 can accept connections from the Internet. 
Access to these machines are allowed from the following local IP address:
156.146.43.11

The other virtual machines within the network can only be accessed by the Jump-Box. 
Access to these machines are only allowed from the following IP address:
10.0.0.4


A summary of the access policies in place can be found in the table below.

|Name     |Publicly Accessible |Allowed IP Addresses |
|---------|--------------------|---------------------|
|Jump-Box |Yes                 |156.146.43.11        |
|Web-1    |No                  |10.0.0.4             |
|Web-2    |No                  |10.0.0.4             |
|ELK4444  |Yes                 |156.146.43.11        |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. 
No configuration was performed manually, which is advantageous 
because setup and troubleshooting are both fast and easy.


The playbook implements the following tasks:

- Install docker.io
- Install pip3
- Install Docker python module
- Increase virtual memory
- Use more memory
- Download and launch a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance:

(Images/elkcontainer.jpg)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 (10.0.0.5) and Web-2 (10.0.0.6)

I installed the following Beats on these machines:
Filebeat and Metricbeat

These Beats allow you to collect the following information from each machine:

Filebeat: monitors set log files, collects data about which files have changed, 
and moves this arranged information to Elasticsearch for future review. 

Metricbeat: monitors and collects system metrics and statistics, 
such as how long a docker container was up for, and moves this 
arranged information to Elasticsearch for future review. 


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible/.
- Update the hosts file in this same directory to include the group name of the ELK server (elk) along with the ELK server's IP address (10.1.0.4).
- Run the playbook, and navigate to http://52.188.212.160:5601/app/kibana to check that the installation worked as expected.
(To see successfully pulled data from the web servers on Kibana, please refer to these screenshots: Images/filebeatdatasuccess.jpg and Images/metricbeatdatasuccess.jpg)
