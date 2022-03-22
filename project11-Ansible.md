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
![](jenkins-ansible.png)

Deploy an Elastic IP Address and attach it to Jenkins-Ansible EC2 Instance

### **Step 2*** – Prepare your development environment using Visual Studio Code ###
