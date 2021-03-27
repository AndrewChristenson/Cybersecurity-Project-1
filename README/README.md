## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

### Cloud Network Diagram
https://github.com/AndrewChristenson/Cybersecurity-Project-1/blob/main/Diagrams/CloudNetworkDiagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

### Filebeat Playbook
https://github.com/AndrewChristenson/Cybersecurity-Project-1/blob/main/Ansible/filebeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
- The Load Balancer distributes network traffic across multiple servers, making Denial of Service attacks less feasible. The advantage of a jump box is it provides one central location to manage the entire environment. The jump box is easier to secure because of the whitelist.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files on the VMs and system metrics.
- Filebeat watches for changes to the files on the VM
- Metricbeat records system metrics

The configuration details of each machine may be found below.

| Name       | Function   | IP Address | Operating System |
|------------|------------|------------|------------------|
| Jump-Box   | Gateway    | 10.0.0.4   | Linux            |
| Web-1      | Web Server | 10.0.0.5   | Linux            |
| Web-2      | Web Server | 10.0.0.6   | Linux            |
| ELK-SERVER | Monitoring | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 173.20.110.223

Machines within the network can only be accessed by each other.
- The Web-1 and Web-2 machines have access and send traffic to the ELK-SERVER VM. Their IP addresses are 10.0.0.5 and 10.0.0.6

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump-Box   | Yes                 | 173.20.110.223       |
| Web-1      | No                  | 10.0.0.4             |
| Web-2      | No                  | 10.0.0.4             |
| ELK-SERVER | No                  | 173.20.110.223       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it reduces the chance of errors and misconfigurations.

The playbook implements the following tasks:
- Installs docker
- Installs docker Python module
- Increases the memory
- Downloads and launches a docker elk container
- Enables service focker on reboot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.



### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 and Web-2

We have installed the following Beats on these machines:
- Filebeat, Metricbeat, and Packetbeat

These Beats allow us to collect the following information from each machine:
- Filebeat: Observes changes to the files. We use it to gather Apache logs.
- Metricbeat: Observes changes in system metrics. We can use it to detect CPU and RAM statistics and login attempts.
- Packetbeat gathers packets as the flow through. This creates a trace of all activity on the network.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to the Ansible Control Node.
- Update the configuration file to include the internal IP addresses and username
- Run the playbook, and navigate to the ELK stack to check that the installation worked as expected.

- The playbook file is install-elk.yml which is copied to the Ansible Control Node
- You update the configuration file to make Ansible run the playbook on a specific machine. 
- The ELK server is installed on an empty machine while filebeat is installed on Web-1 and Web-2 to report to the ELK server.

- The URL you navigate to in order to check that the ELK server is running:
- http://104.42.104.207:5601/app/kibana

