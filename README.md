# TrophyHunterElkStack
A completely configured Elk server setup for use with Filebeat and Metricbeat.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

C:\Users\joehk\Documents\CSB Downloadables\README\README\Images

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select playbook files may be used to install only certain pieces of it, such as Filebeat.

TrophyHunterElkStack/Scripts/TrophyHunt.yml 
TrophyHunterElkStack/Scripts/filebeat-play.yml 
TrophyHunterElkStack/Scipts/metricbeat.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.


The configuration details of each machine may be found below.


| Name                    | Function             | IP Address | Operating System |
|-------------------------|----------------------|------------|------------------|
| Jump Box Provisioner    | Gateway              | 10.0.0.4   | Linux            |
| Web-1                   | DVWA Webserver       | 10.0.0.5   | Linux            |
| Web-2                   | DVWA Webserver       | 10.0.0.6   | Linux            |
| Trophy-Hunter-Elk-Stack | Elk Stack Log Server | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
75.89.241.139
64.33.85.148
71.40.181.35

Machines within the network can only be accessed by the Ansible Container within the Jump Box Provisioner with IP 172.17.0.2.

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Available | Allowed IP Addresses                      |
|----------------------|--------------------|-------------------------------------------|
| Jump-Box-Provisioner | Yes                | 75.89.241.139, 64.33.85.148, 71.40.181.35 |
| Web-1                | No                 | 10.0.0.4/172.17.0.2                       |
| Web-2                | No                 | 10.0.0.4/172.17.0.2                       |
| TrophyHunterElkStack | No                 | 10.0.0.4/172.17.0.2                       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because an automated configuration can be easily changed and
synced to any and all machines on a network

The playbook implements the following tasks:
- Installs Docker.io and python3-pip if its not present on the machines
- Uses the pip module to install the Docker Module if its not present
- Increases the virtual memory available
- Downloads and launches the Elk Docker Container and sets the restart policy so that the container runs on VM startup

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

TrophyHunterElkStack/Diagrams/Elk Container Confirmation.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.5
- Web-2: 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors the logs recorded on the machines, such as authentication logs, audit logs, deprecation logs, and slow logs.
- Metricbeat records system metrics, such as CPU usage, memory usage, inbound traffic, and outbound traffic.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the appropriate playbook file (TrophyHunter.yml, filebeat-play.yml, metricbeat.yml) to /etc/ansible.
- Update the hosts file to include the IPs of your desired machines, add a seperate section for the Elk server(s), titled "Elk" opposed to "webservers" just below the webservers.
- Run the playbook, and navigate to http://[your ip here]:5601/app/kibana to check that the installation worked as expected.
