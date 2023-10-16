## ANSIBLE CONFIGURATION MANAGEMENT – AUTOMATE PROJECT 7 TO 10
### Project Overview



In Projects 7 to 10 we performed a lot of manual operations to set up our virtual servers, install and configure required software anddeploy your web application.

In this Project will make use of DevOps tools to auotmate most of the routine tasks. This will be implemented using Ansible Configuration Management. The desired architecture would be similar to the diagram below:

![image](https://github.com/ettebaDwop/dareyProject11/assets/7973831/a38ab1f6-e682-4185-bffa-2b7331e24ba1)



Bastion server ideology *** ![image](https://github.com/ettebaDwop/dareyProject11/assets/7973831/cf4008de-4b30-48d1-bcc3-3a07ba034c47)  ***



### Task
- Install and configure Ansible client to act as a Jump Server/Bastion Host
- Create a simple Ansible playbook to automate servers configuration

### Step 1 - INSTALL AND CONFIGURE ANSIBLE ON EC2 INSTANCE
1. Update Name tag on the Jenkins EC2 Instance to Jenkins-Ansible.This server would be used to run playbooks.
2. In the  GitHub account create a new repository and name it ansible-config-mgt.

3. To install Ansible run the following code:
 
```
sudo apt update

sudo apt install ansible
```

* Check Ansible version
  
` ansible --version `


![Screenshot (636)](https://github.com/ettebaDwop/dareyProject11/assets/7973831/d7798f28-5144-4a1b-a3ba-fded811e186a)



4. Configure Jenkins build job to save your repository content every time a change is made.

* Create a new Freestyle project ansible in Jenkins and point it to your ‘ansible-config-mgt’ repository.
* Configure Webhook in GitHub and set webhook to trigger ansible build.
* Configure a Post-build job to save all (**) files.
5. Test your setup by making some change in README.MD file in master branch and make sure that builds starts automatically and Jenkins saves the files (build artifacts) in following folder

`ls /var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/`

![image](https://github.com/ettebaDwop/dareyProject11/assets/7973831/bf625200-b926-4582-9479-6ed489827df9)



![Screenshot (672)](https://github.com/ettebaDwop/dareyProject11/assets/7973831/7ca9055d-4aa9-42ba-aafb-ff02c8e415a2)

## Step 2 – PREPARE THE DEVELOPMENT ENVIRONMENT USING VISUAL STUDIO CODE
- Install VS code
- Configure VS code to connect to the newly created GitHub repository.
- Clone down your ansible-config-mgt repo to the Jenkins-Ansible instance run the command:
  
  `git clone <ansible-config-mgt repo link>`

  BEGIN ANSIBLE DEVELOPMENT
In your ansible-config-mgt GitHub repository, create a new branch that will be used for development of a new feature.
Tip: Give your branches descriptive and comprehensive names, for example, if you use Jira or Trello as a project management tool – include ticket number (e.g. PRJ-145) in the name of your branch and add a topic and a brief description what this branch is about – a bugfix, hotfix, feature, release (e.g. feature/prj-145-lvm)

Checkout the newly created feature branch to your local machine and start building your code and directory structure
Create a directory and name it playbooks – it will be used to store all your playbook files.
Create a directory and name it inventory – it will be used to keep your hosts organised.
Within the playbooks folder, create your first playbook, and name it common.yml
Within the inventory folder, create an inventory file (.yml) for each environment (Development, Staging Testing and Production) dev, staging, uat, and prod respectively.
Step 4 – Set up an Ansible Inventory
An Ansible inventory file defines the hosts and groups of hosts upon which commands, modules, and tasks in a playbook operate. Since our intention is to execute Linux commands on remote hosts, and ensure that it is the intended configuration on a particular server that occurs. It is important to have a way to organize our hosts in such an Inventory.

Save below inventory structure in the inventory/dev file to start configuring your development servers. Ensure to replace the IP addresses according to your own setup.

Note: Ansible uses TCP port 22 by default, which means it needs to ssh into target servers from Jenkins-Ansible host – for this you can implement the concept of ssh-agent. Now you need to import your key into ssh-agent:


```
eval `ssh-agent -s`
ssh-add <path-to-private-key>
```
Confirm the key has been added with the command below. Here we should see the name of our key

`ssh-add -l`

Now, ssh into your Jenkins-Ansible server using ssh-agent

`ssh -A ubuntu@public-ip`

Note that our Load Balancer user is ubuntu and user for RHEL-based servers (nfs, web 1 and web 2) is ec2-user.

Update your inventory/dev.yml file with this snippet of code:

```
[nfs]
<NFS-Server-Private-IP-Address> ansible_ssh_user='ec2-user'

[webservers]
<Web-Server1-Private-IP-Address> ansible_ssh_user='ec2-user'
<Web-Server2-Private-IP-Address> ansible_ssh_user='ec2-user'

[db]
<Database-Private-IP-Address> ansible_ssh_user='ec2-user' 

[lb]
<Load-Balancer-Private-IP-Address> ansible_ssh_user='ubuntu'
```
