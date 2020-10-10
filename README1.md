## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/maryrueda/Cybersecurity/blob/main/Diagrams/azure_network.PNG

This document contains the following details:
- Description of the Topology 
- Access Policies
- ELK Configuration
-Beats in Use Including the following:
-Machines Being Monitored
- How to Use the Ansible Build

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Filebeat-Playbook.yml file may be used to install only certain pieces of it, such as Filebeat. Following is an example of teh filebeat-playbook.yml used within the ELK Stack Deployment.


https://github.com/maryrueda/Cybersecurity/blob/main/Ansible/filebeat-playbook.txt



### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing is the process of distributing network traffic across multiple servers. This ensures the availability of resources such as applications and websites.The technology of load balancing assist in maintaining good end-user experiences.
Load balancing works to ensure that the application will be highly available, in addition to restricting inbound access to the network. In this case, the resources being "balanced" are specifically called out as Web1, Web2, and Web3 in the diagram. 
Load balancing ensures that no single server bears too much demand and spreads the incoming traffic evenly and they play a key part in addressing the availability portion of the CIA Triad (Confidentiality, Integrity, Availability). 

The network presented here also includes a Jump Box which is advantages for the follwoing reasons: 
1. The Jump Box prevents additional VM's from being exposed to the public. 
2. The Jump Box is the only VM in the environment that connects two networks (RedTeamNet and ELK_NET) 
3. The Jump Box is the only point of entry to the web servers; allowing for only one open port (SSH port 22). 


Integrating the ELK server allows users to easily monitor the vulnerable VMs for changes to their respective file systems as well as allowing the administrator to obtain system metrics, such as CPU usage. ELK is an acronym for "Elasticsearch," "Logstash," and "Kibana."
Collectively the tool is known as the ELK stack which is comprised of four components, Elasticsearch, Logstash, Kibana, and Beats. Beats includes a combination of technology that proivdes the organization with the ability to collect, parse, monitor, and visualize data as it pertains to each individual client server.
In this case, two separte beats modules are being utilized on the the webservers, Filebeat and Metricbeat.
- "Filebeat is a log shipper belonging to the Beats family- a group of lighweight shippers installed on hosts for shipping different kinds of data into the ELK stack for analysis. Each beat is dedicated to shipping different types of information." https://logz.io/blog/filebeat-tutorial/
Filebeat will monitor the client log files or any location that is specified in the configuration. The beat collects the log events and will forward the events for further analysis. Filebeat is the most popular and commonly used member of the ELK stack as it collects data related to the file system and monitors for suspicious changes. 

- Metricbeat is installed to assist in monitoring the health of each client. This beat collects data pertaining to the operating system and also from services running on the server such as CPU usage. The metrics are real-time and viewable in Kibana.

The configuration details for each machine may be found below. 

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| DVWA1	   | WebServer| 10.0.0.5   | Linux            |
| DVWA2    | WebServer| 10.0.0.6   | Linux            |
| DVWA3    | WebServer| 10.0.0.7   | Linux   	      |
| ELK      | Monitor  | 10.1.0.4   | Linux	      |	

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 71.229.158.82

Machines within the network can only be accessed by eachother. The three virtual machines send traffic (logfiles) to the ELK server via port 9200. 
The following IP address is whitelisted for this network: 71.229.158.82.


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.4             |
| ELK      | No                  | 10.1.0.4             |
| DVWA1    | No                  | 10.0.0.5		|
| DVW2     | No            	 | 10.0.0.6		|
| DVW3     | No		         | 10.0.0.7		|



### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
1. Ansible is a provisioning too which ensures that the provisioning scrips run identically everywhere. Ensuring accuracy and consistency. 
2. Ansible is a provisioning tool that automatically configures VMs or containers; instead of logging into a VM and issuing commands, or editing configuration files manually, Ansible automates these tasks for you, reducing the potential of human error. 
3. Being albe to use an automation tool such as Ansible, allows for efficiency in large scale deployments. 


The Ansible playbook tells Ansible what to do and in this case implements the following:
1. docker.io (docker install which is needed to create, manage, and deliver container applications)
2. python3-pip (pip is the package installer for python); including the docker engine that facilitates the python code to run in the container. 
3. Ansible playbook downloaded and launched the ELK stack container on the server and the Beats" containers on each respective web server. 
The playbook also published the needed ports for the ELK stack:56:01:56:01, 9200:9200, 5044:5044. 

- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

ELK Playbook used can be found here: 

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name     | IP Address |
|----------|-------------
|          |            |
| DVWA1	   | 10.0.0.5   |
| DVWA2    | 10.0.0.6   |
| DVWA3    | 10.0.0.7   | 


We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:

As mentioned previously, "Filebeat is a log shipper belonging to the Beats family- a group of lighweight shippers installed on hosts for shipping different kinds of data into the ELK stack for analysis. Each beat is dedicated to shipping different types of information." https://logz.io/blog/filebeat-tutorial/
Filebeat will monitor the client log files or any location that is specified in the configuration. The beat collects the log events and will forward the events for further analysis. Filebeat is the most popular and commonly used member of the ELK stack as it collects data related to the file system and monitors for suspicious changes. 

- Metricbeat is installed to assist in monitoring the health of each client. This beat collects data pertaining to the operating system and also from services running on the server such as CPU usage. The metrics are real-time and viewable in Kibana.

The Ansible Playbooks can be found here. __________________________________

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the yml file to /etc/ansible directory. 

- Update the hosts file to include the follwoing information:

Web Servers 
 10.0.0.5 ansible_python_interpreter=/usr/bin/python3
 10.0.0.6 ansible_python_interpreter=/usr/bin/python3
 10.0.0.7 ansible_python_interpreter=/usr/bin/python3

ELK Server 
10.1.0.4 ansible_python_interpreter=/usr/bin/python3

Once the hosts file is updated, run the following commands to install filebeat and metricbeat:
$ cd /etc/ansible
$ ansible-playbook install_elk.yml 
$ ansible-playbook install_filebeat.yml
$ ansible-playbook install_metricbeat.yml 


- Open up a browser and navigate to http://[ELK VM IP]:/app/kibana. See image below displaying successful connection to Kibana. 

_____________________________________(insert image of Kibana here) 

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running? http://[ELK VM IP]:/app/kibana
