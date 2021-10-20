#Ansible

Ansible is an open source IT automation engine that automates provisioning, configuration management, application deployment, orchestration, and many other IT processes.

Use Ansible automation to install software, automate daily tasks, provision infrastructure, improve security and compliance, patch systems, and share automation across the organization.

[More details](https://www.redhat.com/en/topics/automation/learning-ansible-tutorial)

**Benefits of Ansible**
* **Free:** Ansible is an open-source tool.
* **Very simple to set up and use:** No special coding skills are necessary to use Ansible’s playbooks.
* **Powerful:** Ansible lets you model even highly complex IT workflows. 
* **Flexible:** You can orchestrate the entire application environment no matter where it’s deployed. You can also customize it based on your needs.
* **Agentless:** You don’t need to install any other software or firewall ports on the client systems you want to automate. You also don’t have to set up a separate management structure.


####Set up guide
**Step 1 — Installing Ansible**
```sh
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt update
$ sudo apt install ansible
```

**Step 2 — generate pub/private key to login node server**
To login worker node from ansible server without providing password we can use servier's public key

```sh
$ ssh-key-gen -b 4096 -t RSA -C my-local-machine
$ ssh-copy-id ansible@ip
```

**Step 3 — Check ansible is working or not**

```sh
$ ansible --version
```

**Step 4 — Configure Ansible server**
Edit /etc/ansible/ansible.cfg file and uncomment inclue hosts file line and then update hosts file with target node details like below

```sh
$ nano /etc/ansible/hosts
```

```dosini
[demo]
node1 ansible_host=10.10.10.5 ansible_ssh_common_args='-o StrictHostKeyChecking=no' ansible_user=ansible
node2 ansible_host=10.10.10.6 ansible_ssh_common_args='-o StrictHostKeyChecking=no' ansible_user=ansible
node3 ansible_host=10.10.10.7 ansible_ssh_common_args='-o StrictHostKeyChecking=no' ansible_user=ansible
```

**Step 5 — Configure Ansible target node**
Login to the target node one by one and then create a user with name ansible and add the new user as sudoers file
```sh
$ sudo adduser ansible
$ sudo visudo
```

End of the file add the below line

```
ansible ALL=(ALL:ALL) NOPASSWD: ALL 
```

#### Useful ansible command

```sh
#show inventory details in yaml format
$ ansible-inventory --list -y               

#ping all host in all groups using ping module in ansible
$ ansible all -m ping

#check playbook syntax
$ ansible-playbook rds_prod.yml  --syntax-check

#Dry-run your playbook
$ ansible demo play-book.yml --check        

#Run ad-hoc command in all host under demo group, only node1, node1 & node2
$ ansible demo -a "df -h"
$ ansible demo[0] -a "df -h"
$ ansible demo[0,1] -a "df -h"

#Run adhoc command
$ ansible all -b -m apt -a "name=apache2 state=present"
$ ansible all -b -m service -a "name=apache2 state=restarted"

#Gather facts
ansible demo[0] -m setup
ansible demo[0] -m setup -a "filter=*ipv4*"
```
