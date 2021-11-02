## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Diagrams/Project 1.drawio.png](https://github.com/faze1096/Project1/blob/ac5c53bfda2efbc13bc77590f0e2e366dc9e36dd/Diagrams/Project1.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  [Playbooks/install-elk.yml](https://github.com/faze1096/Project1/blob/6faf7c55921eda4daf232404555c48204d159c06/Playbooks/install-elk.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

*Load balancing ensures that the application will be highly redundant, in addition to restricting traffic to the network.
* What aspect of security do load balancers protect?
  * It protects attacks against DDoS attacks, protect applications from emerging threats, authenticates user access, and simplifies PCI compliance. 
* What is the advantage of a jump box? 
  * Jumpbox has many different advantages such as having the ability to manager other systems securely and it is acted as a bridge between two trusted networks keeping both secure. 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
 
* What does Filebeat watch for?
  * Filebeat watches for  
Filebeat monitors the log files and locations that you specify and forwards them to Elasticsearch and Logstash for indexing. 
- _TODO: What does Metricbeat record?_
Metricbeat records 
The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address                             | Operating System |
|----------|----------|----------------------------------------|------------------|
| Jump Box | Gateway  | 10.0.0.1(Private)/20.106.161.24(Public)| Linux            |
| Webpage-1|Web Server| 10.1.0.9(Private)                      | Linux            |
| Webpage-2|Web Server| 10.1.0.10(Private)                     | Linux            |
| Webpage-3|Web Server| 10.1.0.11(Private)                     | Linux           |
| ElkServer|Elk Stack | 10.2.0.4(Private)/52.165.170.66(Public)| Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
IP Address: 47.149.144.56

Machines within the network can only be accessed by Jump-Box Provisionser.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
* Jump Box Provisioner
* 10.1.0.4
A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |  47.149.144.56       |
| ElkServer|                     |                      |
| Webpage-1|                     |                      |
| Webpage-2|                     |                      |
| Webpage-3|                     |                      |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- * Install docker.io
- * Install python3-pip
- * Install Docker module
- * Increase virtual memory
- * Use more memory
- * Download and launch a docker elk container
- * Enable service docker on boot 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Images/ElkServer Docker ps](https://github.com/faze1096/Project1/blob/347fd53e21b56b916da59733b0e3202f95e74e64/Images/ELKServer%20Docker%20ps.PNG)
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
