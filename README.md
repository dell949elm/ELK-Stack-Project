## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(https://github.com/zmesdaq/ELK-Stack-Project/blob/main/Diagrams/Diagram%20Elk-%20Stack.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  - filebeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.

- What aspect of security do load balancers protect? What is the advantage of a jump box?
The Load balancer helps distribute traffic evenly across the servers and mitigates DoS attacks. 
Jump box allows us make changes to multiple servers without having to do them individually and is a more secure way to administer tasks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- What does Filebeat watch for? Filebeat watches for auth.logs
- What does Metricbeat record? Metricbeat collects metrics from the operating system and outputs them to Elasticsearch or logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function  | IP Address | Operating System |
|----------|-----------|------------|------------------|
| Jump Box | Gateway   | 10.0.0.4   | Linux            |
| Elk-Stack| SIEM      | 10.1.0.4   | Linux            |
| Web 1    | Webservers| 10.0.0.5   | Linux            |
| Web 2    | Webservers| 10.0.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My home IP address

Machines within the network can only be accessed by SSH or HTTP.
- Which machine did you allow to access your ELK VM? What was its IP address? The ansible container and the Jump box IP address.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses                        |
|----------|---------------------|---------------------------------------------|
| Jump Box | Yes                 | 10.0.0.4                                    |
| Web 1    | No                  | Jump Box IP (SSH) and HTTP anyone can access|
| Web 2    | No                  | Jump Box IP (SSH) and HTTP anyone can access|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible? It give IT administrators more time to focus on other important tasks and allows us to install programs all at the same time.

The playbook implements the following tasks:
- Create and configure the ELK VM
- Install and attach ELK docker container 
- Utilize ansible to deploy the ELK installation into the ELK VM


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(https://github.com/zmesdaq/ELK-Stack-Project/blob/main/Images/docker_ps_output.png.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web 1 10.0.0.5 & Web 2 10.0.0.6

We have installed the following Beats on these machines:
- Metricbeat & Filebeat

These Beats allow us to collect the following information from each machine:
- Metricbeat collects operating systems logs and Filebeat pushes system logs to the Elk stack.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the config file to files folder
- Update the ansible host file to include the web 1 and web 2 VM
- Run the  ansible playbook, and navigate to the web interface Kibana to check that the installation worked as expected

Answer the following questions to fill in the blanks:
- _Which file is the playbook? Where do you copy it? Filebeat-playbook.yml & Metricbeat-playbook.yml and copy it to the /etc ansible file.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? Update the Ansible hosts file. IP groups need to be created (webservers and elkserver)
- _Which URL do you navigate to in order to check that the ELK server is running? ElkVMIP:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
Curl https://du.bootcampcontent.com/denver-coding-bootcamp/du-den-cyber-pt-09-2020-u-c/blob/master/12-Elk-Stack-Project/Activities/Stu_Day_2/Solved/config_files/filebeat-playbook.yml