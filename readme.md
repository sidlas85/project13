## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<img width="599" alt="NEW PROJECT13 PNG" src="https://user-images.githubusercontent.com/101371476/158022890-5745244b-1db0-489a-b9c3-12f5d09939e2.png">

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - /etc/ansible/ELK-install.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly high efficient, in addition to restricting traffic to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?
loadbalancer protects from DDOS attacks by shifting attack traffic.
Load Balancing contributes to the Availability aspect of security in regards to the CIA Triad.
What is the advantage of a jump box?
The advantage of a jump box is to give access to the user from a single node that can be secured and monitored.
The advantage of a JumpBox is the orgination point for launching Administrative Tasks. This ultimately sets the JumpBox as a SAW (Secure Admin Workstation). All Administrators when conducting any Administrative Task will be required to connect to the JumpBox (SAW) before perfoming any task/assignment

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- _TODO: What does Filebeat watch for?_ filebeat watches for any information in the file system which has been changed and when
          filebeat also watch for log files/locations and collect logs data
- _TODO: What does Metricbeat record?
- Metricbeat takes the metrics and statistics that collects and ships them to the output you specify.
  Metricbeat records metric and statistical data from the operating system and from services running on the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| web1     | server   | 10.0.0.8   | ubuntu 20.04     |
| web2     | server   | 10.0.0.9   | ubuntu 20.04     |
| web3/elk | server   | 10.1.0.4   | ubuntu 20.04     |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses? public ip of jumpbox40.122.157.209

Machines within the network can only be accessed by SSH.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?
jumpbox to acess elk vm the private ip is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 40.122.157.209       |
| Web1     |  No                 |                      |
| Web2     |  No                 |                      |
| elk      |  No                 | 20.231.1.149         |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible? It allow you to deploy mutiple server using one playbook

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- install docker container
- install docker.io
  install python-pip
  Launch docker container: elk
  Command: sysctl -w vm.max_map_count=262144

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img width="959" alt="docker ps png" src="https://user-images.githubusercontent.com/101371476/157956459-7c05d9af-e42c-4172-a794-c2f21660e663.PNG">


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring- Web1 10.0.0.8 and Web2  10.0.0.9

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_ filebeat, metricbeat

These Beats allow us to collect the following information from each machine:

<img width="606" alt="filebeat1" src="https://user-images.githubusercontent.com/101371476/157821712-0f4a5a2f-7100-4001-94b4-9ea4ff394bed.PNG">


- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
copy the playbook file to /etc/ansible
update configuration files in include elk vm private ip 10.1.0.4
Run the playbook, and navigate to ElkVM to check that the installation worked as expected. /etc/ansible/host should include

SSH into the control node and follow the steps below:
- Copy the filebeat.yml file to the /etc/ansible/files/ directory.
- Update the  configuration file to include the Private IP of the Elk-Server to the ElasticSearch and Kibana sections of the configuration file.
- Create a new playbook in the /etc/ansible/roles/ directory that will install, drop in the updated configuration file, enable and configure system module, run the filebeat setup, and start the filebeat service.
- Create a new playbook in the /etc/ansible/roles/ directory that will install, drop in the updated configuration file, enable and configure system module, run the metricbeat setup, and start the metricbeat service.
Run the playbooks, and navigate back to the installation page on the ELk-Server GUI, click the check data on the Module Status
Click the verfiy incoming Data to check and see the receiving logs from the DVWA machines.
you should see the following:
<img width="638" alt="metric 1" src="https://user-images.githubusercontent.com/101371476/157827439-6df38962-e86a-42ce-b549-f33302ec969e.PNG">

- Run the playbook, and navigate into the Elk vm, then run docker ps to check that the installation worked as expected.
_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?
  Playbook: install_elk.yml Location: /etc/ansible/install_elk.yml Navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana to confirm ELK and kibana are running. You may need to try from multiple web browsers Click 'Explore On Your Own' and you should see the following:
<img width="617" alt="kibana home" src="https://user-images.githubusercontent.com/101371476/157824291-402f8d78-702c-4fd4-9217-906610535a29.PNG">



_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
