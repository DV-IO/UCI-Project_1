# UCI-Project_1
Contents: UCI Project 1 files to implement and execute AWS Webserver with monitoring.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Map](https://github.com/DV-IO/UCI-Project_1/blob/main/Images/Voorhees-HW12.png?raw=true "Network Map")

These files have been tested and used to generate a live ELK deployment on AWS. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the UCI-Project_1 file may be used to install only certain pieces of it, such as Filebeat.

  - https://github.com/DV-IO/UCI-Project_1/blob/main/Linux/project1-vpc-subnet.yaml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure, in addition to restricting access to the network.
- The benefit of a load balancer, is to protect the server(s) from: DDoS attacks, hacks - thanks to the Web Application Firewall inside of the load balancer, additionally it provides extra user security: a load balancer can request username and password for site access, and (if processing credit cards) can help simplify PCI rules compliance. 
- A Jump Box is advatageous in that it can provide access to the user through a single node, that can be secured and monitored.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system metrics.
- Filebeat – Monitoring for changes to the filesystem. Filebeat utilizes Apache logs for data records.
- Metricbeat – Scans filesystem metrics for changes in (bot not limited to:) CPU usage, SSH attempts, failed sudo escalations, and CPU/RAM stats.

The configuration details of each machine may be found below.

| Name        | Function          | IP Address  | Operating System |
|-------------|-------------------|-------------|------------------|
| Jump Box    | Gateway           | 10.0.0.0/24 | Linux            |
| Webserver 1 | Subnet            | 10.0.0.0/24 | Linux            |
| Webserver 2 | Subnet            | 10.0.1.0/24 | Linux            |
| ELK         | Network Interface | 10.0.0.0/24 | Ubuntu           |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 34.216.240.16

Machines within the network can only be accessed by each other.
- Jump Box can access the ELK server, through port 172.31.3.47

A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible | Allowed IP Addresses |
|-------------|---------------------|----------------------|
| Jump Box    | No                  | 34.216.240.16        |
| Webserver 1 | Yes                 | 10.0.0.0             |
| Webserver 2 | Yes                 | 10.0.1.0             |
| ELK         | No                  | 172.31.3.47          |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- using the configuration can be repeated automatically as new machines are added. Also if updates need to be made the changes can take place in one file and then run to updated the individual machines.

The playbook implements the following tasks:
Install docker
Increase virtual memory
Install python
Install Docker python module
Download and launch a docker container
Enable docker service and open ports: 5601, 5044, 9200

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps output](https://github.com/DV-IO/UCI-Project_1/blob/main/Images/docker-ps-output.png?raw=true)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.0
- 10.0.1.0

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat – Monitoring for changes to the filesystem. Filebeat utilizes Apache logs for data records.
- Metricbeat – Scans filesystem metrics for changes in (bot not limited to:) CPU usage, SSH attempts, failed sudo escalations, and CPU/RAM stats.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file(s) to /etc/ansible.
- Update the ansible.cfg file to include ELK server host information
- Run the playbook, and navigate to http://172.31.3.47:5601/app/kibana to check that the installation worked as expected.

FAQ
- _Which file is the playbook?_ filebeat-playbook.yaml and metric-beat.yaml _Where do you copy it?_ Jump Box machine, docker container: /etc/ansible
- _Which file do you update to make Ansible run the playbook on a specific machine?_ hosts
- _How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ You must update the respective playbook files to determine which machine will receive which software install.
- _Which URL do you navigate to in order to check that the ELK server is running?_ http://172.31.3.47:5601/app/kibana

Relevant commands to aid in execution of DVWA
- sudo docker pull (downloads an ansible docker image)
- sudo docker ps (shows active dockers on a machine)
- sudo docker container list -a (shows all dockers on the server)
- sudo docker start (starts docker)
- sudo docker attach (opens connection to docker)
- ansible all -m ping (ping all of the hosts in the hosts file using the ping module)
- ansible docker-container (the `docker-container` module can be used to download and manage docker containers)
