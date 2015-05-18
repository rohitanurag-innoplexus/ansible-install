 ANSIBLE AUTOMATION By Rohit Anurag


Ansible is an IT automation tool. It can configure systems, deploy software, and orchestrate more advanced IT tasks such as continuous deployments or zero downtime rolling updates.It manages machines in an agentless manner.Ansible by default manages machines over the SSH protocol.

INSTALLATION  -
sudo apt-get install software-properties-common
sudo apt-add repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible


SETUP -
mkdir ansible-install
cd ~/ansible-install/
mkdir Playbook
Move into the new directory  - cd ~/Playbook
Create a new file and called ansible.cfg  and open it for editing - gedit ansible.cfg
Copy the following into the ansible.cfg file, then save and close it - [defaults]
hostfile = hosts
Next, the hosts file needs to be written.Create a hosts file and open it for editing - gedit hosts 
Copy the following into the hosts file - [ubuntumachine] intern@192.168.1.120
Now check if ansible works well or not by pinging to all the IP’s and getting a response - ansible apache -m ping
After doing all the above steps now its time to create a playbook which consists of tasks needs to be performed on nodes.
Playbooks are Ansible’s configuration, deployment, and orchestration language. They can describe a policy you want your remote systems to enforce, or a set of steps in a general IT process.
A very basic Ansible playbook is a single yaml file which specifies the host group and one or more tasks to be run on the hosts within the specified group.
Firstly we will start with making and running a basic playbook which installs the latest version of apache2.
STEPS -
Create a apache2.yml file in Playbook directory - gedit apache2.yml
It has been created in the file inside the folder.Do check it.
It will contain  the following codes - 
---
- hosts: apache
  sudo: yes
  tasks:
    - name: install apache2
      apt: name=apache2 update_cache=yes state=latest
Now run the playbook which will install apache2 in all nodes mentioned in hosts file created earlier.
One problem faced by this is that the sudo password of all the hosts should be same. Work is in progress in addressing that problem.
Run Playbook - ansible-playbook apache2.yml --ask-sudo-pass.
After running it succesfully do check it if apache is installed in all nodes.
This is a simple playbook creation and running tutorial.
In the folder there are five playbooks which installs and setups the software and modules.
perldrivers.yml - This one first installs CPAMN in the nodes mentioned and and also sees if GCC is present. After installing , it nows loads 	different perl modules as mentioned in the file - Mongodb,CGI,JSON,Encode,Spreadsheet::XLSX
php5.yml -  installs php5 latest version.
mysql.yml - installs mysql servers and clients and also configures the username and password in the hosts for the mysql using this playbook.
mongodb.yml - installs mongodb latest release .
npmnodejs.yml - install nodejs and npm packages in nodes.
apache2.yml - installs apache2 latest version .
gruntandbower.yml - Firstly install npm and nodejs package by calling npmnodejs.yml and then run this playbook to install grund and bower nodejs packages.
REFERENCES -   1> Digital Ocean Tutorial http://bit.ly/1BD1wHD ,
                        2> Ansible Documentation    http://bit.ly/1AeW3MZ
