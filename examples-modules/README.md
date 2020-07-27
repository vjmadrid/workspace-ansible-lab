# examples-modules

This project is a repository of examples / exercises to **practices** with some of the **modules** of **Ansible**





## Prerequisites

Define which elements are necessary to use the examples

* Ansible installed
* Define your own inventory file with the name : "inventory.txt"
* Define your own inventory file with the name : "ansible.cfg"
* Define your own inventory file with the name : "hosts" (used ansible.cfg)
* The inventory file should have a grouping of hosts named "all_targets"

**Example "inventory.txt"**

```bash
ansible-target-1 ansible_host=IP_1
ansible-target-2 ansible_host=IP_2

[all_targets]
ansible-target-1
ansible-target-2 
```

**Example "ansible.cfg"**

```bash
[defaults]
allow_world_readable_tmpfiles = True
host_key_checking = False
retry_files_enabled = False
inventory = ./hosts
roles_path = ./roles
```




## Examples

* Setup Module
* Ping Module
* Command Module
* Shell Module
* Reboot Module
* User Module
* File Module
* Copy Module
* Replace Module
* Lineinfile Module
* Manager Software Package Module (yum for CentOs)
* Service Module




## Setup Module

**Example 1 : Show Facts**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m setup
```

**Example 2 : Show Specific Fact**

Execute the following command

```bash
# Case 1
ansible all_targets -i inventory.txt -m setup | grep distribution_version

# Case 2
ansible all_targets -i inventory.txt -m setup | grep distribution

# Case 3
ansible all_targets -i inventory.txt -m setup -a filter=distribution_version

# Case 4
ansible all_targets -i inventory.txt -m setup -a filter=distribution_version
```





## Ping Module

**Example 1 : Pinging the grouped hosts**

Execute the following command (with specific inventory)

```bash
ansible all_targets -i inventory.txt -m ping
```

Execute the following command (with specific ansible.cfg)

```bash
ansible all_targets -m ping
```

Execute the following command (with all)

```bash
ansible all -i inventory.txt -m ping
```


**Example 2 :  Pinging the grouped hosts with NO GATHERING Parameter**

Execute the following command

```bash
ANSIBLE_GATHERING=explicit ansible all -i inventory.txt -m ping
```


**Example 3 :  Pinging the grouped hosts with NO GATHERING Environment Variable**

Execute the following commands

```bash
export ANSIBLE_GATHERING=explicit
```

```bash
ansible all -i inventory.txt -m ping
```


**Example 4 :  Pinging the grouped hosts with NO GATHERING Environment Variable Script**

Execute the following commands

Create script : shell-script.sh with

```bash
export ANSIBLE_GATHERING=explicit
```

Configure 

```bash
chmod 755 shell-script.sh
```

Execute 

```bash
./shell-script.sh
```

Execute 

```bash
ansible all -i inventory.txt -m ping
```





## Command Module

**Example 1 : Shows the hostname of the grouped hosts**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m command -a 'hostname'
```

**Example 2 : Shows the uptime of the grouped hosts**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m command -a 'uptime'
```

**Example 3 : Shows hosts**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m command -a 'cat /etc/hosts'

or

ansible all_targets -i inventory.txt -a 'cat /etc/hosts'
```





## Shell Module

**Example 1 : Generates a file with the output of the execution of the command 'ls -l'**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m shell -a 'ls -l > temp.txt'
```

Verify 

```bash
ssh ansible-target-1

ls

exit
```

**Example 2 : Show the contents of the previously generated file**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m command -a 'cat temp.txt'
```


**Example 3 : Show the contents of use a disk**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m command -a 'df -h'
```





## Reboot Module

**Example 1 : Reboot the grouped hosts**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m reboot --become
```





## User Module

**Example 1 : Create new user 'test'**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m user -a 'name=test password=changeit2020 groups=ansible shell=/bin/bash' --become
```

Verify 

```bash
ssh ansible-target-1

cat /etc/passwd

su test

exit
```

**Example 2 : Delete user 'test'**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m user -a 'name=test state=absent remove=yes force=yes' --become
```





## File Module

**Example 1 : Create new file 'example.txt'**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m file -a 'dest=/home/ansible/example.txt state=touch mode=600 owner=ansible group=ansible'
```

Verify

```bash
ssh ansible-target-1

ls

exit
```

**Example 2 : Delete file 'example.txt'**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m file -a 'dest=/home/ansible/example.txt state=absent'
```

Verify

```bash
ssh ansible-target-1

ls

exit
```

**Example 3 : Create directory '/home/ansible/example'**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m file -a 'dest=/home/ansible/example state=directory mode=755'
```

Verify

```bash
ssh ansible-target-1

ls

exit
```

**Example 4 : Delete directory '/home/ansible/example'**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m file -a 'dest=/home/ansible/example state=absent'
```

Verify

```bash
ssh ansible-target-1

ls

exit
```




## Copy Module

**Example 1 : Copy file**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m copy -a 'src=/home/ansible/example.txt dest=/home/ansible/result.txt remote_src=yes'
```

```bash
ssh ansible-target-1

ls

exit
```

**Example 2 : Copy content to a file**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m copy -a 'content="Hello World!\n" dest=/home/ansible/result.txt remote_src=yes'
```

```bash
ssh ansible-target-1

cat result.txt

exit
```





## Replace Module

**Example 1 : Replace all instances of a string**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m replace -a "path=/home/ansible/result.txt regexp='World' replace='Test'"
```

```bash
ssh ansible-target-1

cat result.txt

exit
```





## Lineinfile Module

**Example 1 : Add New Line**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m lineinfile -a "path=/home/ansible/result.txt line='Description' create=yes"
```

Verify

```bash
ssh ansible-target-1

cat result.txt

exit
```

**Example 2 : Replace all instances of a string**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m lineinfile -a "path=/home/ansible/result.txt regexp='Description' line='Description Updated'"
```

Verify

```bash
ssh ansible-target-1

cat result.txt

exit
```





## Manager Software Package (yum for CentOs)

**Example 1 : Install package 'git'**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m yum -a 'name=git state=present' --become

or 

ansible all_targets -i inventory.txt -m yum -a 'name=git state=latest' --become
```

Verify

```bash
ansible all_targets -i inventory.txt -m shell -a 'git --version'
```

**Example 2 : Uninstall package 'git'**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m yum -a 'name=git state=absent' --become
```

Verify

```bash
ansible all_targets -i inventory.txt -m shell -a 'git --version'
```

Command not found





## Service Module

Note : install service "httpd"

```bash
# Install
ansible all_targets -i inventory.txt -m yum -a 'name=httpd state=present' --become

#Uninstall
ansible all_targets -i inventory.txt -m yum -a 'name=httpd state=absent' --become
```

Verify

```bash
ssh ansible-target-1

systemctl status httpd

exit
```

**Example 1 : Start 'httpd' Service**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m service -a 'name=httpd state=started' --become
```

**Example 2 : Stop 'httpd' Service**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m service -a 'name=httpd state=stopped' --become
```

**Example 3 : Restart 'httpd' Service**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m service -a 'name=httpd state=restarted' --become
```










## Authors

* **Víctor Madrid**