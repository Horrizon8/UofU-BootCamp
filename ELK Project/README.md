# Automated-ELK-Stack-Deployment-Project-1

Jared Smith
2021/03/01
U of U - Cybersecurity Boot Camp

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Project 1 Red-Team Network Diagram](https://github.com/Horrizon8/UofU-BootCamp/blob/main/ELK%20Project/Diagrams/Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

[filebeat-playbook.yml](https://github.com/Horrizon8/UofU-BootCamp/blob/main/ELK%20Project/Ansible/filebeat_playbook.yml)

[filebeat-configuration.yml](https://github.com/Horrizon8/UofU-BootCamp/blob/main/ELK%20Project/Ansible/filebeat-configuration.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

- Load balancing ensures that the application will be highly functional, in addition to restricting traffic to the network.

- What aspect of security do load balancers protect? 
  - Load Balancers help prevent overloading servers as well as optimizes productivity and maximizes uptime. 
	- Load Balancers also add redundancy by re-routing live traffic to multiple servers causing the elimination of single points of failure.

- What is the advantage of a jump box?
  - A JumpBox is normally a highly secured computer that is used only for administrative tasks. 
	- JumpBoxes were developed to secure administrative workspaces to decrease the chances of infection and unauthorized access.

- Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
  
- What does Filebeat watch for?
  - It monitors the log files/locations that you specify and forwards them to Elasticsearch/Logstash for indexing.
 
- What does Metricbeat record?
  - It records metrics/statistics data of VM's and exports them to the daskboard in Elasticsearch/Logstash.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Primary Server | 10.0.0.5   | Linux            |
| Web-2    | Secondary Server | 10.0.0.6   | Linux            |
| Web-3    | Teriary Server | 10.0.0.7   | Linux            |
| ELK Host | ELK Server | 10.1.0.4 | Linux |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 184.170.240.106 (My Local Host Public IP)

Machines within the network can only be accessed by the Jump Box.
- Jump Box (10.0.0.4)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes | 184.170.240.106 |
| Web-1    | No | 10.0.0.4 |
| Web-2    | No | 10.0.0.4 |
| Web-3    | No | 10.0.0.4 |
| ELK Host | Yes | 184.170.240.106 & 10.0.0.4 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

- What is the main advantage of automating configuration with Ansible?
	- Playbooks. A few lines of code and all your coneected machines can have new programs installed or updated.

The playbook implements the following tasks:

- Installs Docker
- Installs PIP3
- Installs Docker-Python
- Increases and expands the system memory
- Downloads/Installs/Launches the ELK docker container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[ELK Docker PS](https://github.com/Horrizon8/UofU-BootCamp/blob/main/ELK%20Project/Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- List the IP addresses of the machines you are monitoring
  - Web-1 (10.0.0.5)
  - Web-2 (10.0.0.6)
  - Web-3 (10.0.0.7)

We have installed the following Beats on these machines:
- FileBeat
- MetricBeat

These Beats allow us to collect the following information from each machine:
- Filebeat is used to collect log files of any/all programs from the remote machines.
	- Ex. Apache system logs and MySQl databases.	
- Metricbeat collects machine metrics such as CPU type/usage/uptime, memory usage and OS type.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

---Filebeat---

- Copy the filebeat-configuration.yml file to /etc/ansible/roles/files.
- Update the filebeat-configuration.yml file to include the ELK private IP in lines 1106 and 1806.
- Run the playbook, and navigate to http://(ELK-VM Public IP):5601/ to check that the installation worked as expected.

---Metricbeat---

- Copy the metricbeat-configuration.yml file to /etc/ansible/roles/files.
- Update the metricbeat-configuration.yml file to include the ELK private IP in lines 62 and 96.
- Run the playbook, and navigate to http://(ELK-VM Public IP):5601/ to check that the installation worked as expected.

### Quick Reference

- _Which file is the playbook? filebeat-playbook.yml
- Where do you copy it?_ /etc/ansible/roles
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ /etc/ansible/hosts 
- _Which URL do you navigate to in order to check that the ELK server is running? http://(ELK-VM Public IP):5601/
