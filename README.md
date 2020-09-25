## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Network Topology](CybersecurityProjects/Images/FAMReddNetworkTopology.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

[MetricFilebeat.yml file](CybersecurityProjects/Resources/MetricFilebeat.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive, in addition to restricting DDoS attacks to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system logs.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name      | Function | IP Address   | Operating System |
|-----------|----------|--------------|------------------|
| Jump Box  | Gateway  |23.100.43.42  | Linux            |
| Web-1     | DVWA     |10.0.0.5      | Linux            |
| Baloo-1   | Elk      |10.1.0.4      | Linux            |
|Workstation| Host     |73.202.206.232| Windows          |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
73.202.206.232

Machines within the network can only be accessed by SSH from the Ansible Docker container on the Jump-Box machine.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 73.202.206.232       |
| DVWA     | No                  | 23.100.43.42         |
| ELK      | No                  | 23.199.43.42         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because playbooks
in Ansible can be used again to configure other machines.

The playbook implements the following tasks:
- Download the .deb file for filebeat
- Install the .deb file for filebeat
- Copy the configuration file from the Ansible container to your virtual machine
- Then run the commands 'filebeat modules enable system', 'filebeat setup', and 'filebeat -e'

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ElkSetup001](CybersecurityProjects/Images/ElkSetup001.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5, Web-2 10.0.0.6, and Web-3 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat will log changes to files in your configured virtual machines and send them to Kibana.
Metricbeat will log metric data from your virtual machines and send them to Kibana.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the .yml file to /etc/ansible/roles.
- Update the config.yml file to include the the group of target machines 
- Run the playbook, and navigate to Kibana (http://{insert your jump box ip address}:5601/app/kibana to check that the installation worked as expected.

*As a note: You will use the 'nano' command to configure your playbook files. And you will use the 'ansible-playbook' command to run your yml files.
