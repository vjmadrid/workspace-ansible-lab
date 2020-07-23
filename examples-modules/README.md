# examples-modules

This project is a repository of examples / exercises to **practices** with some of the **modules** of **Ansible**





## Prerequisites

Define which elements are necessary to use the examples

* Ansible installed
* Define your own inventory file with the name : "inventary.txt"
* The inventory file should have a grouping of hosts named "all_targets"





## Examples

* Ping Module
* Setup Module
* Command Module
* Shell Module
* Reboot Module
* User Module
* File Module
* Copy Module
* Manager Software Package Module (yum for CentOs)
* Service Module




## Setup Module

**Example 1 : Pinging the grouped hosts**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m ping
```





## Setup Module

**Example 1 : Show Facts**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m setup
```

**Example 2 : Show Specific Fact**

Execute the following command

```bash
# Case 1
ansible all_targets -i inventary.txt -m setup | grep distribution_version

# Case 2
ansible all_targets -i inventary.txt -m setup | grep distribution

# Case 3
ansible all_targets -i inventary.txt -m setup -a filter=distribution_version

# Case 4
ansible all_targets -i inventary.txt -m setup -a filter=distribution_version
```






## Command Module

**Example 1 : Shows the hostname of the grouped hosts**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m command -a 'hostname'
```

**Example 2 : Shows the uptime of the grouped hosts**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m command -a 'uptime'
```





## Shell Module

**Example 1 : Generates a file with the output of the execution of the command 'ls -l'**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m shell -a 'ls -l > temp.txt'
```

**Example 2 : Show the contents of the previously generated file**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m command -a 'cat temp.txt'
```

**Example 3 : Show the contents of use a disk**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m command -a 'df -h'
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
ansible all_targets -i inventary.txt -m user -a 'name=test password=changeit2020' --become
```

**Example 2 : Delete user 'test'**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m user -a 'name=test state=absent' --become
```





## File Module

**Example 1 : Create new file 'example.txt'**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m file -a 'dest=/home/ansible/example.txt state=touch mode=600 owner=ansible group=ansible'
```

**Example 2 : Delete file 'example.txt'**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m file -a 'dest=/home/ansible/example.txt state=absent'
```

**Example 3 : Create directory '/home/ansible/example'**

Execute the following command

```bash
ansible all_targets -i inventory.txt -m file -a 'dest=/home/ansible/example state=directory mode=755'
```

**Example 4 : Delete directory '/home/ansible/example'**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m file -a 'dest=/home/ansible/example  state=absent'
```




## Copy Module

**Example 1 : Copy File**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m file -a 'src=/home/ansible/example.txt dest=/home/ansible/result.txt'
```





## Manager Software Package (yum for CentOs)

**Example 1 : Install package 'git'**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m yum -a 'name=git state=present' --become

or 

ansible all_targets -i inventary.txt -m yum -a 'name=git state=latest' --become
```

**Example 2 : Uninstall package 'git'**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m yum -a 'name=git state=absent' --become
```




## Service Module

**Example 1 : Start 'httpd' Service**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m service -a 'name=httpd state=started' --become
```

**Example 2 : Stop 'httpd' Service**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m service -a 'name=httpd state=stopped' --become
```

**Example 3 : Restart 'httpd' Service**

Execute the following command

```bash
ansible all_targets -i inventary.txt -m service -a 'name=httpd state=restarted' --become
```










## Authors

* **Víctor Madrid**