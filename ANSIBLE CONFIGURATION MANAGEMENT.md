## ANSIBLE CONFIGURATION MANAGEMENT – AUTOMATE PROJECT 7 TO 10



### Task
- Install and configure Ansible client to act as a Jump Server/Bastion Host
- Create a simple Ansible playbook to automate servers configuration

### INSTALL AND CONFIGURE ANSIBLE ON EC2 INSTANCE
Update Name tag on your Jenkins EC2 Instance to Jenkins-Ansible. We will use this server to run playbooks.
In your GitHub account create a new repository and name it ansible-config-mgt.

* To install Ansible run the following code:
 
```
sudo apt update

sudo apt install ansible
```

* Check Ansible version
  
` ansible --version `

