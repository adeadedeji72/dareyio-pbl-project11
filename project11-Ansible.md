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

4. Configure Jenkins build job to save your repository content every time you change it – this will solidify your Jenkins configuration skills acquired in Project 9.
  * Create a new Freestyle project ansible in Jenkins and point it to your *‘ansible-config-mgt’* repository.
  * Configure Webhook in GitHub and set webhook to trigger ansible build.
  * Configure a Post-build job to save all (**) files, like you did it in Project 9.
 
Test your setup by making some change in README.MD file in master branch and make sure that builds starts automatically and Jenkins saves the files (build artifacts) in following folder
~~~
ls /var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/
~~~
Note: Trigger Jenkins project execution only for /main (master) branch.

Now your setup will look like this:
![](jenkins_ansible.png)

Deploy an Elastic IP Address and attach it to Jenkins-Ansible EC2 Instance

### **Step 2*** – Prepare your development environment using Visual Studio Code ###
Install Visual Studio Code software on your local machine, then connect to your new Github repo

### **BEGIN ANSIBLE DEVELOPMENT** ###

1. In your ansible-config-mgt GitHub repository, create a new branch that will be used for development of a new feature.

Tip: Give your branches descriptive and comprehensive names, for example, if you use Jira or Trello as a project management tool – include ticket number (e.g. PRJ-145) in the name of your branch and add a topic and a brief description what this branch is about – a bugfix, hotfix, feature, release (e.g. feature/prj-145-lvm)

1. Checkout the newly created feature branch to your local machine and start building your code and directory structure
1. Create a directory and name it playbooks – it will be used to store all your playbook files.
1. Create a directory and name it inventory – it will be used to keep your hosts organised.
1. Within the playbooks folder, create your first playbook, and name it common.yml
1. Within the inventory folder, create an inventory file (.yml) for each environment (Development, Staging Testing and Production) dev, staging, uat, and prod respectively.

### **Step 4** – Set up an Ansible Inventory ###
An Ansible inventory file defines the hosts and groups of hosts upon which commands, modules, and tasks in a playbook operate. Since our intention is to execute Linux commands on remote hosts, and ensure that it is the intended configuration on a particular server that occurs. It is important to have a way to organize our hosts in such an Inventory.

Save below inventory structure in the inventory/dev file to start configuring your development servers. Ensure to replace the IP addresses according to your own setup.

##Note: Ansible uses TCP port 22 by default, which means it needs to ssh into target servers from Jenkins-Ansible host – for this you can implement the concept of ssh-agent. Now you need to import your key into ssh-agent:
~~~
eval `ssh-agent -s`
ssh-add <path-to-private-key>
~~~
Confirm the key has been added with the command below, you should see the name of your key
~~~
ssh-add -l
~~~
Now, ssh into your Jenkins-Ansible server using ssh-agent
~~~
ssh -A ubuntu@public-ip
~~~
Update your inventory/dev.yml file with this snippet of code:
~~~
[nfs]
<NFS-Server-Private-IP-Address> ansible_ssh_user='ec2-user'

[webservers]
<Web-Server1-Private-IP-Address> ansible_ssh_user='ec2-user'
<Web-Server2-Private-IP-Address> ansible_ssh_user='ec2-user'

[db]
<Database-Private-IP-Address> ansible_ssh_user='ec2-user' 

[lb]
<Load-Balancer-Private-IP-Address> ansible_ssh_user='ubuntu'
~~~
Also notice, that your Load Balancer user is ubuntu and user for RHEL-based servers is ec2-user.

Update your inventory/dev.yml file with this snippet of code:
