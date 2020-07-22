# examples-playbooks

This project is a repository of examples / exercises to **practices** with some **playbooks** of **Ansible**





## Prerequisites

Define which elements are necessary to use the examples

* Ansible installed
* Define your own inventory file with the name : "inventary.txt"
* The inventory file should have a grouping of hosts named "all_targets"





## Examples

* Basic Playbook
* Setup Module
* Command Module
* Shell Module
* Reboot Module
* User Module
* File Module
* Copy Module
* Manager Software Package Module (yum for CentOs)
* Service Module




## Basic Playbook

**Example 1 : Print Hello World**

Step to follow:

* Create "basic-hello-world.yml"

```bash
---
- name: Print Hellow World
  hosts: all_targets
  tasks:
  - debug:
      msg: "Hello World!"
```

* Execute the following command

```bash
ansible-playbook -i inventary.txt  playbooks/basic-hello-world.yml --syntax-check

# Check
ansible-playbook -i inventary.txt  playbooks/basic-hello-world.yml --check

ansible-playbook -i inventary.txt playbooks/basic-hello-world.yml
```













## Authors

* **Víctor Madrid**