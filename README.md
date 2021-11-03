## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Diagrams/Project 1.drawio.png](https://github.com/faze1096/Project1/blob/747ea324854221db68c8b0d7da0eac95b6f3b469/Diagram/Project%201%20Diagram.drawio.png)

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
* What does Metricbeat record?_
  * Metricbeat is used to monitor and collect data such as system CPU, memory and load in a docker environment
 
The configuration details of each machine may be found below.

| Name     | Function | IP Address                             | Operating System |
|----------|----------|----------------------------------------|------------------|
| Jump Box | Gateway  | 10.0.0.1(Private)/20.106.161.24(Public)| Linux            |
| Webpage-1|Web Server| 10.1.0.9(Private)                      | Linux            |
| Webpage-2|Web Server| 10.1.0.10(Private)                     | Linux            |
| Webpage-3|Web Server| 10.1.0.11(Private)                     | Linux            |
| ElkServer|Elk Stack | 10.2.0.4(Private)/52.165.170.66(Public)| Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
IP Address: 47.149.144.56

Machines within the network can only be accessed by Jump-Box Provisionser.
* Which machine did you allow to access your ELK VM? 
  * Jump Box Provisioner
* What was its IP address?
  * 10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |       Yes           |  47.149.144.56       |
| ElkServer|       No            |  10.1.0.4            |
| Webpage-1|       No            |  10.1.0.4            |
| Webpage-2|       No            |  10.1.0.4            |
| Webpage-3|       No            |  10.1.0.4            |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
* Installs docker.io
* Installs python3-pip
* Installs Docker module
* Increases virtual memory
* Uses more memory
* Downloads and launches a docker elk container
* Enables service docker on boot 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Images/ElkServer Docker ps](https://github.com/faze1096/Project1/blob/347fd53e21b56b916da59733b0e3202f95e74e64/Images/ELKServer%20Docker%20ps.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
* Webpage-1: 10.1.0.9
* Webpage-2: 10.1.0.10
* Webpage-3: 10.1.0.11

We have installed the following Beats on these machines:
* Filebeats
* Metricbeats

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
* Filebeat collects 
* Metricbeat collects
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-configuration.yml file to /etc/ansible
- Update the filebeat-configuration.yml file to include the Elk Server's Private IP(10.2.0.4) in lines 1106 and 1806.
- Run the playbook, and navigate to http://52.165.170.66:5601/

- Copy the metricbeat-configuration.yml file to /etc/ansible
- Update the metricbeat-configuration.yml file to include the Elk Server's Private IP(10.2.0.4) in lines 62 and 95.
- Run the playbook, and navigate to http://52.165.170.66:5601/
- 
_TODO: Answer the following questions to fill in the blanks:_
Filebeat and Metricbeat:
* Which file is the playbook?
  * filebeat-playbook.yml and metricbeat-playbook.yml
* Where do you copy it?
  * /etc/ansible/roles
* Which file do you update to make Ansible run the playbook on a specific machine?
  * /etc/ansible/hosts
* How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
  * I specified in the /etc/ansible/hosts file. One group is "webservers" which has the VMs that I installed Filebeat on. The other group is "Elk" which will have the Elk Server VM IP address that will have the ELK installed. 
* Which URL do you navigate to in order to check that the ELK server is running?
  * http://52.165.170.66:5601/

##Bonus

Filebeat:
-To create the filebeat-configuration.yml file, run, and then nano the filebeat-config.yml : curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/filebeat-config.yml 
-To create the playbook: nano filebeat-playbook.yml

---
- name: installing and launching filebeat
  hosts: webservers
  become: yes
  tasks:

  - name: download filebeat deb
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb

  - name: install filebeat deb
    command: dpkg -i filebeat-7.4.0-amd64.deb

  - name: drop in filebeat.yml
    copy:
      src: /etc/ansible/filebeat-config.yml
      dest: /etc/filebeat/filebeat.yml

  - name: enable and configure system module
    command: filebeat modules enable system

  - name: setup filebeat
    command: filebeat setup

  - name: start filebeat service
    command: service filebeat start

  - name: enable service filebeat on boot
    systemd:
      name: filebeat
      enabled: yes

-To run the playbook(make sure you are in the directory that holds the file) : ansible-playbook filebeat-playbook.yml
-Navigate to:http://52.165.170.66:5601/ to ensure the playbook ran correctly. 

Metricbeat:
-To create the metricbeat-configuration.yml file, run, and then nano the metricbeat-config.yml : curl https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat > /etc/ansible/metricbeat-config.yml
-To create the playbook: nano metricbeat-playbook.yml

---
- name: installing and launching metricbeat
  hosts: webservers
  become: yes
  tasks:

  - name: download metricbeat deb
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.4.0-amd64.deb

  - name: install metricbeat deb
    command: dpkg -i metricbeat-7.4.0-amd64.deb

  - name: drop in metricbeat.yml
    copy:
      src: /etc/ansible/metricbeat-config.yml
      dest: /etc/metricbeat/metricbeat.yml

  - name: enable and configure system module
    command: metricbeat modules enable docker

  - name: setup metricbeat
    command: metricbeat setup

  - name: start metricbeat service
    command: service metricbeat start

  - name: enable service metricbeat on boot
    systemd:
      name: metricbeat
      enabled: yes
      
-To run the playbook(make sure you are in the directory that holds the file) : ansible-playbook metricbeat-playbook.yml
-Navigate to:http://52.165.170.66:5601/ to ensure the playbook ran correctly. 
