# Scripts
Linux &amp; Ansible Scripts GW Cyber Security
# Cloud Network
This is a collection of Linux Scripts and Ansible Scripts from my CyberClass.

Most of the scripts are used to configure cloud servers with different docker containers.

The final setup was 4 servers running vulnerable DVWA containers along with a jump box and a server running an ELK stack container.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](https://github.com/pdanny90/p_dan/blob/main/diagrams/Diagram_1.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

[Filebeat Playbook](https://github.com/pdanny90/p_dan/blob/main/ansible/roles/filebeat-playbook.yml)

[Metricbeat Playbook](https://github.com/pdanny90/p_dan/blob/main/ansible/roles/metricbeat-playbook.yml)

[DVWA Playbook](https://github.com/pdanny90/p_dan/blob/main/ansible/pentest.yml)

[Elk Playbook](https://github.com/pdanny90/p_dan/blob/main/ansible/install-elk.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

- Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
The benefits to a load balancer can add layers of security such as protection against DDoS and authenticate user access. They are also easy to scale and can increase performance and response time.

- Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.
Filebeat is then used as a logging agent that is often used to monitor data and forwards it to a centralized location like Elasticsearch or Logstash. However, metricbeat on the other hand helps to measure the behavior and monitors the usage of a system's resources and also forwards them to Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| JumpBox  | Gateway  | 10.0.0.1   | Linux  Ubuntu 18.04 LTS |
| Elk      | ElkStack | 10.1.0.4   | Linux  Ubuntu 18.04 LTS |
| Web 1    | Server   | 10.0.0.5   | Linux  Ubuntu 18.04 LTS |
| Web 2    | Server   | 10.0.0.6   | Linux  Ubuntu 18.04 LTS |
| Web 3    | Server   | 10.0.0.7   | Linux  Ubuntu 18.04 LTS |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Elk Stack and Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
  
-  Public Host IP **100.36.98.117**

Machines within the network can only be accessed through the JumpBox.
  
-  Private IP **10.0.0.4**

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 100.36.98.117        |
| Elk      | Yes                 | 100.36.98.117        |
| Web 1    | No                  | 10.0.0.4             |
| Web 2    | No                  | 10.0.0.4             |
| Web 3    | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
Using Ansible serves a variety of benefits that allows one to easily administer tasks across machines such as configuring and installing applications. This lightweight method consumes less resources and greatly negates human error during configuration. Through the use of containers and applications allows administrators to have the most flexibility to reproduce an environment across various systems, detect vulnerabilities and review logs.

The playbook implements the following tasks:

1. First, the playbook was configured to install docker.io and python3.
2. Second, ensure that docker is successfully running by running sudo systemctl status docker.
3. Last, run the Elk Container.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](https://github.com/pdanny90/p_dan/blob/main/elk_images/elk.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- **Web 1: 10.0.0.5**

- **Web 2: 10.0.0.6**

- **Web 3: 10.0.0.7**

We have installed the following Beats on these machines:

- **Metricbeat**

- **Filebeat**

These Beats allow us to collect the following information from each machine:

- **Filebeat is used to pass information of the systems logs from the Web virtual machines in friendly readable format**

- **Metricbeat then reports the system's metrics such as how many resources the machines are using.**


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
  
      *Copy the elk-stack-playbook.yml file to /etc/ansible.*
  
      *Update the hosts file to include the Elk's virtual machine's IP address.*
  
      *Run the playbook, and navigate to http://20.114.172.178:5601/app/kibana to check that the installation worked as expected.*

---

1. Which file is the playbook? Where do you copy it?
  
    **filebeat-playbook.yml** and then copied to **/etc/ansible/roles** directory

2. Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ 

  **hosts** file and within the same hosts file one should have the web servers and a separate group for the elk server.

3. Which URL do you navigate to in order to check that the ELK server is running?
  
    Check by going to: **http://20.114.172.178:5601/app/kibana**
