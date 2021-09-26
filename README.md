## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![ELK STACK DIAGRAM](https://github.com/Hjavid123/Azure-cloud-security-project-1/tree/main/Images)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the __YAML(Playbooks)__ file may be used to install only certain pieces of it, such as Filebeat.

 [filebeat-playbook.yml](https://github.com/Hjavid123/Azure-cloud-security-project-1/blob/main/Ansible/filebeat-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly __secured and reliable and accessible__, in addition to restricting __access___ to the network.
- _TODO:_
- What aspect of security do load balancers protect? __Availiability__
- What is the advantage of a jump box?__Jump box is the only machin that are coneccted and have access to our network's Vms for configuratione, and it is  restricted by Sec_Rules and SSh_Keys and as a Gatekeeper for the whole network. We just need to harden only one machine, no matter how big or small our network is.__  
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the __files___ and system __metrics___.
- TODO: What does Filebeat watch for?__Collects data about the file system and monitor files for suspicious changes.__
- TODO: What does Metricbeat record?__collects machine metrics, such as uptime__

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.9   | Linux            |
| Web-1     |  DVWA-Server        |  10.0.0.10          |Linux                  |
| Web-2    |   DVWA-Server       |    10.0.0.11        |  Linux                |
| Web-3    |  DVWA-Server|10.0.0.4 |Linux
ELK-Vm     |     ELK-Monitoring-Server     |  10.1.0.4          |      Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the __ELK__ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- TODO:_Add whitelisted IP addresses:__
- __MY-Home-IP-Address.(by it's SSH-key-Public)__
- __Jump Box PrivatIP: 10.0.0.9__

Machines within the network can only be accessed by    __Jump-Box-Vm___.
- TODO: Which machine did you allow to access your ELK VM?   __JUMP-BOX__
-  What was its IP address?  __10.0.0.9__

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses |
|----------  |---------------------|----------------------|
| Jump Box   | No              | My-Home-IP     |
| Web-1 Web-2 Web-3           |   No                  | Jump-Box_Private-IP:10.0.0.9 and PublicIP:20.150.136.168                     |
| ELK-Server         |     No                | MY-Home-IP-Address.(by it's SSH-key-Public),Jump Box PrivatIP: 10.0.0.9  
                     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?__dramatically **improved scalability,We can add and configure many machine very fast and simple.__

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- __Configure Elk VM with Docker__...
- __Install *dockerio*__
- __Install pip3__

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK-docker_ps_output](https://github.com/Hjavid123/Azure-cloud-security-project-1/blob/main/Images/ELK-docker_ps_output.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- __Web-1 : 10.0.0.10__
- __Web-2 : 10.0.0.11__
- __WEb-3: 10.0.0.4__

We have installed the following Beats on these machines:
- __Filebeats.__
- __Metricbeats.__

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
-  __METRICBEAT :__
- __collects machine metrics, such as uptime(Uptime is a measure of how long a machine has been on. Servers are generally expected to be available for a certain percentage of the time, so analysts typically track uptime to ensure your deployments meet service-level agreements (SLAs))__,__A metric is simply a measurement about an aspect of a system that tells analysts how "healthy" it is.__

- __FILEBEAT : Collects data about the file system and monitor files for suspicious changes._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the __playbook.yml__ file to __/etc/ansible/ Folder.__
- Update the __ansible.cfg__ file to include: 
-__1- Name of the playbook or services.__
-__2- Ips and ports for machines.__

- Run the playbook, and navigate to __ELK-VM__ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook?__YAML files with .yml__ Where do you copy it?_ __In ansible container in etc folder of the Jump-Box machine (provisioner) in which we want to config and install services.__ 
- _Which file do you update to make Ansible run the playbook on a specific machine?__hosts__ How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
-  __[webservers]__
__10.0.0.10 ansible_python_interpreter=/usr/bin/python3
10.0.0.11 ansible_python_interpreter=/usr/bin/python3
10.0.0.4 ansible_python_interpreter=/usr/bin/python3__

  - __[elk]__
  __10.1.0.4 ansible_python_interpreter=/usr/bin/python3__

- _Which URL do you navigate to in order to check that the ELK server is running?
__ - `http://(myhome)IP:5601/app/kibana`__

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc_
  Run: `curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/filebeat-playbook.yml`
  

    metricbeat modules enable docker
    
    metricbeat setup

