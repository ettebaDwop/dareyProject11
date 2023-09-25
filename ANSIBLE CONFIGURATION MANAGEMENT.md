## ANSIBLE CONFIGURATION MANAGEMENT – AUTOMATE PROJECT 7 TO 10



### Task
- Install and configure Ansible client to act as a Jump Server/Bastion Host
- Create a simple Ansible playbook to automate servers configuration

### INSTALL AND CONFIGURE ANSIBLE ON EC2 INSTANCE
1. Update Name tag on the Jenkins EC2 Instance to Jenkins-Ansible.This server would be used to run playbooks.
2. In the  GitHub account create a new repository and name it ansible-config-mgt.

3. To install Ansible run the following code:
 
```
sudo apt update

sudo apt install ansible
```

* Check Ansible version
  
` ansible --version `

4. Configure Jenkins build job to save your repository content every time you change it – this will solidify your Jenkins configuration skills acquired in Project 9.

* Create a new Freestyle project ansible in Jenkins and point it to your ‘ansible-config-mgt’ repository.
* Configure Webhook in GitHub and set webhook to trigger ansible build.
* Configure a Post-build job to save all (**) files, like you did it in Project 9.
5. Test your setup by making some change in README.MD file in master branch and make sure that builds starts automatically and Jenkins saves the files (build artifacts) in following folder

`ls /var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/`
