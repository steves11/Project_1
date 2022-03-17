# Project_1

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Diagram/Networkdiagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

  - filebeat-playbook.yml
  - metricbeat-playbook.yml
  - elk-install.yml
  - ansible-playbok.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessable, in addition to restricting traffic to the network.
- A load balancer defends against distributed denial-of-service (DDoS) attacks. Load balancers directs traffic to ensure that network doesnt get overwhelmed from high traffic. The advanyage of having a jumpbox allows is that it as an extra layer of security, by allowing anyone who needs to preform administrative task, first has to  log into the jumpbox first before being allowed to execute anything on the network.   

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system traffic.
- Filebeat monitors for log files or places which you specify, collects log events, and forwards them to Elasticsearch 
- Metricbeat- records all the metrics on operating systems and services on the server. Ex: CPU usages

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System      |  
|----------|----------|------------|-----------------------|  
| Jump Box | Gateway  | 10.0.0.4   | Linux Ubuntu 18.04    |
| ELK      | Elk-stack| 10.2.0.4   | Linux Ubuntu 18.04    |
| Web-1    | Webserver| 10.0.0.7   | Linux Ubuntu 18.04    |
| Web-2    | Webserver| 10.0.0.8   | Linux Ubuntu 18.04    |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 68.82.54.31

Machines within the network can only be accessed by Jumpbox.
- Jumpbox 13.82.4.176

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |     yes             | 68.82.54.31          |
| Web-1    |     no              | 10.0.0.4 13.82.4.176 |
| Web-2    |     no              | 10.0.0.4 13.82.4.176 |
| Elk      |     yes             | 10.0.0.4 68.82.54.31 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage of automating configuration on Ansilbe is that you can easily build and tare them down 

The playbook implements the following tasks:
- Install Docker.io and pip3
- Increase the memory of vm change value 262144
- Install Downlaod and run conatainer
- Set published ports 5601:5601 9200:9200 5044:5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
(Images/docker_ps_output.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.7 Web-1
- 10.0.0.8 Web-2

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Metricbeat records all the metrics from operaring systems and services on the server such as cpu usage and filebeat keeps logs for any change done to a file. (elasticsearch) 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:t 
- Copy the configured files (metricbeat.conf.yml filebeat.conf.yml)  to /etc/ansible .
- Update the cofnfigured files to include the private ip of the elk server. (change under elastic search and kibana)
- Run the playbook, and navigate to elk-servers-publicip:5601/app/kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? elk-install.yml metricbeat-playbook.yml filebeat-playbook.yml
-  Where do you copy it? /etc/ansible
- _Which file do you update to make Ansible run the playbook on a specific machine? /etc/ansible/hosts
-  How do I specify which machine to install the ELK server on versus which to install Filebeat on? When creating the playbook you specify where you are applying,webservers or elkservers with their ip addresses.
- _Which URL do you navigate to in order to check that the ELK server is running? elk-servers-publicip:5601/app/kibana
