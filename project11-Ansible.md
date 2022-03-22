# **ANSIBLE CONFIGURATION MANAGEMENT – AUTOMATE PROJECT 7 TO 10** #

ANSIBLE CONFIGURATION MANAGEMENT – AUTOMATE PROJECT 7 TO 10

Ansible Client as a Jump Server (Bastion Host)
A Jump Server (sometimes also referred as Bastion Host) is an intermediary server through which access to internal network can be provided. 
If you think about the current architecture you are working on, ideally, the webservers would be inside a secured network which cannot be 
reached directly from the Internet. That means, even DevOps engineers cannot SSH into the Web servers directly and can only access it through 
a Jump Server – it provide better security and reduces attack surface.

On the diagram below the Virtual Private Network (VPC) is divided into two subnets – Public subnet has public IP addresses and Private subnet 
is only reachable by private IP addresses.


### **Tasks** ###
1. Install and configure Ansible client to act as a Jump Server/Bastion Host
1. Create a simple Ansible playbook to automate servers configuration

### **INSTALL AND CONFIGURE ANSIBLE ON EC2 INSTANCE** ###
1. Update Name tag on your Jenkins EC2 Instance to Jenkins-Ansible. We will use this server to run playbooks.
1. In your GitHub account create a new repository and name it ansible-config-mgt.
1. Instal Ansible
~~~
sudo apt update
sudo apt install ansible
~~~
