# classprojects
class projects repositry
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/Project-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.
- (Ansible/filebeat-playbook.yml)
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Load balancer protects availability aspect of security. Jump box can sit in a DMZ and be a originating point for accessing internal secured network form public (insecure) network. It provides a buffer for securely accessing servers

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the metric logs and system logs
- _TODO: What does Filebeat watch for? Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing
- _TODO: What does Metricbeat record? Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash

File beat dashboard screenshots can be seen here here
(Images/filebeat-dashboard.png)

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name      |  Function | IP Address | Operating System |
|---------- |----------|------------|------------------|
| Jump-VM|   Jump Box | 10.0.0.1   | Linux            |
| Elk-Server| elk stak| 10.1.0.4   | Linux            |
| Web-1     | DVWA    | 10.0.0.5   | Linux            |
| Web-2     | DVWA    | 10.0.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-VM machine can accept SSH connections from the Internet. Access to this machine is only allowed from the following IP addresses: 69.181.24.29
- 

Machines within the network can only be accessed by docker conatiner runiing on Jump-VM. SSH access to ELK VM ia allowed from Jump-VM (10.1.0.4) through docker conatinesr


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes  SSH            | 69.181.24.29         |
|Elk-Server| Yes http/5601       | 69.181.24.29         |
| Web-1    | NO                  | 10.1.0.4             |
| Web-2    | No                  | 10.1.0.4             |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because you can use ansible to Change the configuration of an application, OS, or device; start and stop services; install or update applications; implement a security policy; or perform a wide variety of other configuration tasks on multiple machines with one configuration file

The playbook implements the following tasks:
Following steps in play book install docker conatiner and download & install elk container image
-  Use apt module
    - name: Install docker.io
      apt:
        update_cache: yes
        name: docker.io
        state: present

- Use docker_container module
    - name: download and launch a docker elk container
      docker_container:
        name: elk
        image: sebp/elk:761
        state: started
        restart_policy: always
        published_ports:
          - 5601:5601
          - 9200:9200
          - 5044:5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/ELK-docker-image.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 IP 10.0.0.5 and Web-2 10.0.0.6

We have installed the following Beats on these machines:
- Following beats were installed on these machines:
  # Use command module
  - name: install metricbeat
    command: dpkg -i metricbeat-7.4.0-amd64.deb

Metric Playbook](Ansible/metric-betat-playbook.yml.md)
Metric Beat Config Screenshot (Images/metric-beat-config-yml.png)
Metric Beat Config Screenshot (mages/metric-beat-config-yml2.png)
Metric Beat Playbook Screenshot (mages/metric-beat-playbook-yml.png)
Metric Beat Playbook Install Screenshot (mages/metric-beat-play-book-install.png)


These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below for file beat install:
- Copy the  file to filebeat-config.yml to etc/ansible/files
- Update the filebeat-config.yml file to include hosts and setup.kibana entries
- File Beat Config Screenshot (Images/file-beat-config-yml.png)
- File Beat Config Screenshot (mages/file-beat-config-yml2.png)
- Run the playbook, and navigate to http://40.117.145.102:5601/app/kibana to check that the installation worked as expected.
- Kiabana portal screenshot (Images/Kiabana-Portal.png)
- File Beat Play Book Screenshot (Images/file-beat-playbook-yml.png)
- File Beat Play Book Install (images/file-beat-playbook-yml-install.png)
- File Beat Data Check (images/systemlog-data-check.png)

ELK Deployment:
- _Which file is the playbook? elk.yml is playbook file and copy it to /etc/ansible
- you will update Ansible hosts file to add entry for Elk server:

[webservers]
10.0.0.5 ansible_python_interpreter=/usr/bin/python3
10.0.0.6 ansible_python_interpreter=/usr/bin/python3

# List the IP address of your ELK server
# There should only be one IP address
[elk]
10.1.0.4 ansible_python_interpreter=/usr/bin/python3
_
- _Which URL do you navigate to in order to check that the ELK server is running?
http://40.117.145.102:5601/app/kibana

