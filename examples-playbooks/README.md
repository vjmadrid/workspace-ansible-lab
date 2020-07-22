# examples-playbooks

This project is a repository of examples / exercises to **practices** with some **playbooks** of **Ansible**





## Prerequisites

Define which elements are necessary to use the examples

* Ansible installed
* Define your own inventory file with the name : "inventary.txt"
* The inventory file should have a grouping of hosts named "all_targets"





## Examples

* Basic Playbook
* File Playbook
* User Playbook





## Basic Playbook

**Example 1 : Print Hello World**

Step to follow:

* Create "basic-hello-world.yml" file in playbooks

```bash
---
- name: Print Hellow World
  hosts: all_targets
  tasks:
  - debug:
      msg: "Hello World!"
```

* Execute the following command (examples-playbooks/)

```bash
# Syntax-check
ansible-playbook -i inventary.txt  playbooks/basic-hello-world.yml --syntax-check

# Check
ansible-playbook -i inventary.txt  playbooks/basic-hello-world.yml --check

# Execute
ansible-playbook -i inventary.txt playbooks/basic-hello-world.yml
```


**Example 2 : Print Facts**

Step to follow:

* Create "basic-print-facts.yml" file in playbooks

```bash
---
- name: Print Hellow World
  hosts: all_targets
  tasks:
  - debug:
      msg: "Hello World!"
```

* Execute the following command (examples-playbooks/)

```bash
ansible-playbook -i inventary.txt playbooks/basic-print-facts.yml
```





## File Playbook

**Example 1 : Create File**

Step to follow:

* Create "file-create-empty-file.yml" file in playbooks

```bash
---
- name: Create Empty File 'example-txt'
  hosts: all_targets
  become: true
  tasks:
  - name: Create Empty File
    file:
        path: "/home/ansible/example.txt"
        state: touch
```

* Execute the following command (examples-playbooks/)

```bash
ansible-playbook -i inventary.txt playbooks/file-create-empty-file.yml
```


**Example 2 : Create Directory**

Step to follow:

* Create "file-create-directory.yml" file in playbooks

```bash
---
- name: Create Directory 'example'
  hosts: all_targets
  become: true
  tasks:
  - name: Create Directory
    file:
        path: "/home/ansible/example"
        state: directory
        mode: 755
        owner: ansible
        group: ansible
```

* Execute the following command (examples-playbooks/)

```bash
ansible-playbook -i inventary.txt playbooks/file-create-directory.yml
```




## User Playbook

**Example 1 : Create "test" user**

Step to follow:

* Create "user-create-test-user.yml" file in playbooks

```bash
---
- name: Create 'test' user
  hosts: all_targets
  become: true
  tasks:
  - name: Create User
      user: 
        name: test 
        password: changeit2020 
        groups: ansible 
        shell: /bin/bash
```

* Execute the following command (examples-playbooks/)

```bash
ansible-playbook -i inventary.txt playbooks/user-create-test-user.yml
```


**Example 2 : Delete "test" user**

Step to follow:

* Create "user-delete-test-user.yml" file in playbooks

```bash
---
- name: Delete 'test' user
  hosts: all_targets
  become: true
  tasks:
  - name: Delete user
      user: 
        name: test 
        state: absent
        remove: yes
        force: yes
```

remove : delete home directory
force : delete all files 


* Execute the following command (examples-playbooks/)

```bash
ansible-playbook -i inventary.txt playbooks/user-delete-test-user.yml
```





## Authors

* **Víctor Madrid**