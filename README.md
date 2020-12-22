# cyberrepo
Cybersecurity Bootcamp Repository of Nell-e Medina

Cybersecurity Class

Compiled in this repository are some of the activities and homework exercises that we have done in the Cybersecurity bootcamp class. 

In the Ansible directory, you will find three (3) playbooks that were used to configure the ansible containers and the playbooks to install and configure the filebeat and metricbeat applications. 

In the Linux directory you will find a collection of bash scripts I have written as part of our exercises and homeworks in the class. 

In the Diagrams directory you will find network architecture diagrams created using draw.io as part of our exercises during the weeks of Networking. The one labeled "Virtual Network Infrastructure - DVWA instances on VMs" is a diagram of a virtual network we built to explore firewall configurations. The diagram labeled "Elk Diagram" is a representation of the establishment of the ELK server with the virtual network and a network peering function in order to monitor the virtual machines. 

The following narratives below will guide you on the design and implementation of the ELK stack:

## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.

https://github.com/nell-e/cyberrepo/blob/main/Diagrams/ELK%20Diagram%20(1).JPG

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the myplaybook2elk.yml file and filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

   https://github.com/nell-e/cyberrepo/blob/main/Ansible/filebeat-playbook.yml
   
This document contains the following details:
Description of the Topology
Access Policies
ELK Configuration
Beats in Use
Machines Being Monitored
How to Use the Ansible Build

### Description of the Topology

 The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly secure, in addition to restricting access to the network.

- What aspect of security do load balancers protect? What is the advantage of a jump box? 
Load balancers help protect the Availability of network servers.  A jump box is a secure computer that all admins first connect to before launching any administrative task or use as an origination point to connect to other servers or untrusted environments.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system data.

- What does Filebeat watch for? 

Filebeat helps generate and organize log files to send to Logstash and Elasticsearch. Specifically, it logs information about the file system, including which files have changed and when.Filebeat is often used to collect log files from very specific files, such as those generated by Apache, Microsoft Azure tools, the Nginx web server, and MySQL databases.Since Filebeat is built to collect data about specific files on remote machines, it was installed on the web VMS being monitored. 

- What does Metricbeat record? 

Metricbeat collects machine metrics, such as uptime. A metric is simply a measurement about an aspect of a system that tells analysts how "healthy" it is.
Common metrics include:
CPU usage: The heavier the load on a machine's CPU, the more likely it is to fail. Analysts often receive alerts when CPU usage gets too high.
Uptime: Uptime is a measure of how long a machine has been on. Servers are generally expected to be available for a certain percentage of the time, so analysts typically track uptime to ensure your deployments meet service-level agreements (SLAs).
In other words, Metricbeat makes it easy to collect specific information about the machines in the network. Filebeat enables analysts to monitor files for suspicious changes.

The configuration details of each machine may be found below.
 
| Name 	| Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump box | Gateway  | 10.0.0.6   | Linux            |
| elk 	|  VM      |  10.2.0.4  | Linux            |
| Web-1	|  VM      | 10.0.0.7   | Linux            |
| Web-2 	|  VM       |  10.0.0.8 | Linux            |
| Web-3 	|  VM       |  10.0.0.9 | Linux            |
 
### Access Policies
 
The machines on the internal network are not exposed to the public Internet.
 
Only the ELK machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Whitelisted IP addresses: 99.98.161.163
 
Machines within the network can only be accessed via the jump-box provisioner.
- Which machine did you allow to access your ELK VM? What was its IP address? 10.0.0.6

A summary of the access policies in place can be found in the table below.

| Name 	| Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box  | No             	   | 99.98.161.163   	  |
|   elk   	| No 	               | 10.0.0.6			      |             	
|   web-1 	| No               	| 10.0.0.6              |
|   web-2   | No 	               | 10.0.0.6			      |             	
|   web-3 	| No               	| 10.0.0.6              |

### Elk Configuration

Ansible was used to automate the configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible? All functions (ie. starting, updating, and installing) are performed autonomously.
 
The playbook implements the following tasks:

After the VM was created for the ELK server it was added to the ansible hosts file 
Created a new ansible-playbook to configure our new ELK VM
The playbook installed docker.io, python3-pip, and docker.
After Docker is installed, download and run the sebp/elk:761    container.
After the ELK container is installed, SSH to your container and double-check that your elk-docker container is running.
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance. 
  
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
web-1 10.0.0.12
web-2 10.0.0.13
web-3 10.0.0.17

Installed the following Beats on these machines:
Filebeat
Metricbeat
 
These Beats allow to collect the following information from each machine:

Filebeat monitors the log files or locations that you specify.
Metricbeat collects metrics from the system and services running on the server.

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
SSH into the control node and follow the steps below:

- Copy the ansible configuration file to the container.
- Update the hosts file to include the three web VM’s IP addresses.
- Run the playbook, and navigate to  http://[your.VM.IP]:5601/app/kibana to check that the installation worked as expected.

This is the command to run the playbook:

 ansible-playbook myplaybook2elk.yml


Below is a sample findings from using Kibana established through the ELK server:


Diagram :https://drive.google.com/file/d/1MAhXze4uWWBvHWH3OTnslo7gPg6GhBkC/view?usp=sharing

Kibana Findings
Source IP of the Unique Visitor using a number of bytes that is considerably higher than all other usages: 
35.143.166.159

The geo coordinates of this activity was:  
{ "lat": 43.34121, "lon": -73.6103075 }

Source Machine OS: Windows 8

URL accessed: https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-6.3.2-i686.rpm

Visitor’s traffic originated from Facebook
This event appears to be a user downloading a Linux package from the website being monitored.
Linux packages are not typically malicious but they could be. Depending on the website, this could be harmless traffic from a sysadmin performing an update.
The main concern is the referral link from Facebook, as it's probably not within compliance to post package update links on Facebook.
This user could be further investigated and monitored for suspicious activity.
