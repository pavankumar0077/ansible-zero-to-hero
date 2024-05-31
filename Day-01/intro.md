INSTALL ANSIBLE 
--
``` https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#control-node-requirements ```

![image](https://github.com/pavankumar0077/ansible-zero-to-hero/assets/40380941/3b068ffd-48c2-4109-8aa7-cf0c14b81ed7)

- Chef
- Puppet
- Ansible
- Salt

![image](https://github.com/pavankumar0077/ansible-zero-to-hero/assets/40380941/3734051b-6a43-493f-8436-8060d20c8a26)

History :
--
- Every ORG will have SYSTEM ADMINS --> they used to work on CONFIG MANAGEMENT ---> Mostly manaully activity - it is creating issues to the Sys Admins
- Be'coz types or SERVER like -- Linux, Debian, Apline and Windows
- They to make OS update to data, System dependencies are up todate, App'n software up todate. and Server == THEY HAVE MAKE UP TODATE FOR ALL THE SOFTWARES
- If SysAdmin wants to update Java version in Linux, and other OS he has to login into each OS, Running in different platform and make it UP TODATE which is not that easy.
- TO SOLVE THIS PROBLEM WE HAVE PUPPET, CHEF, SALT AND ANSIBLE.

PUPPET & CHEF
--
- It will act as an INTERFACE between PHYSICAL SERVERS AND VM's
- SYSAMDINS should has to learn Puppet or Chef and WRITE THE SCRIPTS, It will works as an INTERFACE and it will AUTOMATE THE TARGET SERVERS.

CHALLENGES WITH PUPPET & CHEF 
--
- The learning crave is not that easy.
- They SHOULD LEARN RUBBY, AND COMPLEX ARCHITECUTRE OF PUPPET & CHEF.
- THEY ARE NOT AGENT LESS IN THE ARCHITECTURE  -  SysAdmin should go to each of the Physcial Server or VM's they need to INSTALL AGENT IN ALL THE TARGET SERVER.

ANSIBLE
--

![image](https://github.com/pavankumar0077/ansible-zero-to-hero/assets/40380941/d24e8f1a-a41a-4683-85b9-2cff494319b7)

- TO SOLVE THE ABOVE PROBLEMTS ANSIBLE CAME INTO THE PICTURE.
- Now sysAdmin should know only YAML, and ANSIBLE IS **AGENTLESS** ( No need to install any software in the traget servers )
- 1. CONTROL NODE == THE MACHINE WHERE YOU INSTALL THE ANSIBLE SOFTWARE IS CALLED CONTROL NODE ( IT CAN BE PHYSCIAL SERVER OR A VM )
- 2. MANAGE NODE == THESE ARE THE TARGET MACHINE WHERE CONTROL NODE TRIES TO UPDATE OR CONFIGURE THE SYSTEM
- IF THERE IS A TASK TO INSTALL JAVA IN 100 SERVERS, WE WILL WRITE A ANSIBLE SCRIPT YAML FILE AND WILL USE CONTROL NODE AND RUN A COMMAND USING THAT COMMAND IT WILL TALK TO ALL THE TARGET SERVERS AND INSTALL JAVA.
- COOL THING IS. MANAGE NODES ( TARGET SERVERS ) CAN BE ANYTHING LIKE WINDOWS, MAC, LIUNX, CENTOS AND ETC.
- TARGET NODES SHOULD HAVE PYTHON, ANSIBLE WILL TALK TO TARGET SERVERS USING PYTHON.

WHAT EXACTLY ANSIBLE IS ? 
==

![image](https://github.com/pavankumar0077/ansible-zero-to-hero/assets/40380941/fb467692-b588-4668-b9d9-2258d4067902)

- IT IS CONFIGURATION MANAGEMENT TOOL
- IT IS POWERFUL AUTOMATION PLATFORM
- IT IS USEF FOR PROVISIONING ( create resources on cloud platforms, like ec2 instance creation, s3 and etc .. )
- IT IS ALSO USED AS DEPLOYMENT ( CI CD ) - For example if they want to deploy an application in kubernetes clusters or multiple vm's they can also use ANSIBLE FOR THAT.
- IT IS ALSO FOR NETWORK AUTOMATION - For example - Companies like CISCO, F5 they have they load balancer, they have security related tools, API Gateways -- THEY HAVE NETWORK APPLIANCES CAN BE PHYSICAL or VIRTUAL, WE CAN ALSO TALK TO LOAD BALANACERS OR NETWORK APPLIANCES OF CISOC, F5 AND ETC COMPANIES -- WE CAN AUTOMATE THEY NETWORK APPLIANCES, VERY SIMPLE AUTOMATION OF A VLAN.

![image](https://github.com/pavankumar0077/ansible-zero-to-hero/assets/40380941/7d43a706-9444-46c4-9064-8f066077203b)

ANSIBLE VS SHELL SCRIPTING VS PYTHON
--
- Shell scripting -- To install java, Automate using script script
- Python -- We can automate java installation in a virtual machine using python.
- Ansible -- By using ansible we can do the same task - automate.

### To do this task which one we have to choose
-- **TASK**: INSTALL JAVA ON TARGETE SERVER, 5 VM'S 
-- WE ARE WRITE A **SHELL SCRIPT** AND RUN IN 5 VM'S -- IT WORKS FINE,BUT IF THE VM is windows then the automation will mot work. May be different VM's WILL HAVE DIFFERENT PACKAGE MANAGER., --- SHELL SCRIPT IS NOT SITABLE FOR THIS TASK.

-- PYTHON IS SUITABLE FOR THIS TASK, IT WORKS FINE ON ANY DEVICE LIKE WINDOWS & UBUNTU AND ETC. -- IT WORKS FINE.
-- 1. We need to know python
-- 2. Updating the python scripts ( May after any year script -- syntax or functions may change )
-- 3. We cam use paramiko or fabric to install in multiple vm's -- but we need to learn it. it takes time.

-- ANSBILE
- 1. WE DON'T NEED TO LOGIN INTO EACH AND EVERY MACHINE.
  2. INSTALL ANISBLE IN THE CONTROL-NODE AND TELL THE MANAGE NODES -- WHICH ARE IN INVENTORY FILE 
  3. IT WILL DO PARALLEL OR SEQUENTIALLY AND COMPLETE THE TASK.
  4. JUST NEED TO LEARN YAML THAT'S IT.

### NOTE : WE NEED TO USE ANSIBLE OVER SHELL AND PYTHON.

WHEN CAN WE USE PYTHON OVER ANSIBLE
--
- WHEN YOUR TASK IS TO TALK TO APIs
- like if you want to create a github issues or a jira ticket using their API, then go with PYTHON.

![image](https://github.com/pavankumar0077/ansible-zero-to-hero/assets/40380941/2397c0af-fe17-4c08-aea3-152c7e20f8f5)

PROVISIONING
--
- ANSIBLE CAN BE USED FOR PROVISIONING
- TERRAFOROM IS ALSO USED FOR PROVISIONING. WHICH ONE SHOULD I NEED TO USE.
- ANSIBLE OR TERRAFORM.
- ANSIBLE CORE SKILL - CONFIGURATION MANAGEMENT
- TERRAFORM CORE SKILL - INFRA STRUCTURE AS A CODE.


PYTHON IS MUST TO RUN ANSIBLE
--
- ON CONTROL NODE -- PYTHON MUST BE INSTALLED
- ON MANAGE NODES -- PYTHON MUST BE INSTALLED.
- ANSIBLE TAKES THE YAML FILE --> IT CONVERTS YAML FILE INTO PYTHON --> AND IT EXECUTES THE PYTHON MODULES ON THE MANAGE NODES.
- IT CONNECTS TO THE MANAGE NODES --> USING SSH PROTOCAL (if it is LINUX), IF IT IS WINDOWS THEN IT WILL USE **WINRM PROTOCAL**
