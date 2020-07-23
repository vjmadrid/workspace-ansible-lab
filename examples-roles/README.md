# examples-roles

This project is a repository of examples / exercises to **practices** with some **roles** of **Ansible**





## Prerequisites

Define which elements are necessary to use the examples

* Ansible installed
* Define your own inventory file with the name : "inventory.txt"
* The inventory file should have a grouping of hosts named "all_targets"

**Example "inventory.txt"**

```bash
ansible-target-1 ansible_host=IP_1
ansible-target-2 ansible_host=IP_2

[all_targets]
ansible-target-1
ansible-target-2 
```





## Examples

* Instal Roles 


### Install Roles

* Execute the following command (examples-roles/)

```bash
ansible-playbook -i inventory.txt  playbooks/prepare.yml
```


## Problem "Expecting a 'map', but found a 'sequence'" Visual Studio Code

Step to follow:

* Install Ansible Extension [https://marketplace.visualstudio.com/items?itemName=vscoss.vscode-ansible](https://marketplace.visualstudio.com/items?itemName=vscoss.vscode-ansible)

* Change settings

```bash
"files.associations": {
    "**/*.yml": "ansible"
},
"ansible.validation": true
```








## Authors

* **Víctor Madrid**