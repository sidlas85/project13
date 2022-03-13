## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<img width="599" alt="NEW PROJECT13 PNG" src="https://user-images.githubusercontent.com/101371476/158046262-fa36ce18-a6b5-4f64-8331-1443265ab10f.png">

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
| Jump Box | Yes/No              | 10.0.0.4             |
| Web1     |  No                 | 10.0.0.8             |
| Web2     |  No                 | 10.0.0.9             |
| elk      |  No                 | 10.1.0.4             |
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
SSH into the control node and follow the steps below:

copy the playbook file to /etc/ansible
update configuration files in include elk vm private ip 10.1.0.4
Run the playbook, and navigate to ElkVM to check that the installation worked as expected. /etc/ansible/host should include

[webservers] [10.1.0.9] ansible_python_interpreter=/usr/bin/python3 [10.1.0.10] ansible_python_interpreter=/usr/bin/python3 [10.1.0.11] ansible_python_interpreter=/usr/bin/python3

[elk] [10.0.0.4] ansible_python_interpreter=/usr/bin/python3

Run the playbook, and SSH into the Elk vm, then run docker ps to check that the installation worked as expected. Playbook: install_elk.yml Location: /etc/ansible/install_elk.yml Navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana to confirm ELK and kibana are running. You may need to try from multiple web browsers Click 'Explore On Your Own' and you should see the following:

<img width="617" alt="kibana home png" src="https://user-images.githubusercontent.com/101371476/158046172-23315b82-c42d-4527-a17d-3e7ab2e6172a.PNG">
Answer the following questions to fill in the blanks:

Which file is the playbook? Where do you copy it? /etc/ansible/file/filebeat-configuration.yml
Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ edit the /etc/ansible/hosts file to add webserver/elkserver ip addresses
Which URL do you navigate to in order to check that the ELK server is running? http://[your.ELK-VM.External.IP]:5601/app/kibana
Using the Playbook-filebeat-playbook.yml

Copy the filebeat.yml file to the /etc/ansible/files/ directory.

Update the configuration file to include the Private IP of the Elk-Server to the ElasticSearch and Kibana sections of the configuration file.

Create a new playbook in the /etc/ansible/roles/ directory that will install, drop in the updated configuration file, enable and configure system module, run the filebeat setup, and start the filebeat service.

Create a new playbook in the /etc/ansible/roles/ directory that will install, drop in the updated configuration file, enable and configure system module, run the metricbeat setup, and start the metricbeat service.

Run the playbooks, and navigate back to the installation page on the ELk-Server GUI, click the check data on the Module Status

Click the verfiy incoming Data to check and see the receiving logs from the DVWA machines.

you should see the following:
<img width="638" alt="metric png" src="https://user-images.githubusercontent.com/101371476/158046226-893238a7-7b6a-4c07-9e4b-27a0711c90a9.PNG">
The commands needed to run the Ansible configuration for the Elk-Server are:

- ssh azadmin@JumpBox(Public IP)
- sudo docker container list -a (locate your ansible container)
- sudo docker start container (name of the container)
- sudo docker attach container (name of the container)
cd /etc/ansible/ - ansible-playbook elk.yml (configures Elk-Server and starts the Elk container on the Elk-Server) wait a couple minutes for the implementation of the Elk-Server - cd /etc/ansible/roles/ - ansible-playbook filebeat-playbook.yml (installs Filebeat and Metricbeat) - open a new web browser (http://[your.ELK-VM.External.IP]:5601/app/kibana) This will bring up the Kibana Web Portal - check the Module status for file beat and metric beat to see their data receiving.

** You will need to ensure all files are properly placed before running the ansible-playbooks.

