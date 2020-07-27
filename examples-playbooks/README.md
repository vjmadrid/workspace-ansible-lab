# examples-playbooks

This project is a repository of examples / exercises to **practices** with some **playbooks** of **Ansible**





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

**Simple**

* Basic Playbook
* Ping Playbook
* Reoot Playbook
* File Playbook
* User Playbook
* Replace Playbook (Mix: )
* Archive Playbook
* Manager Software Package Module (yum for CentOs) / Service Module

**Complex**

* Install JDK





## Simple

### Basic Playbook

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

* Execute the following command (examples-playbooks/simple/basic/)

```bash
# Syntax-check
ansible-playbook -i inventory.txt  playbooks/simple/basic/basic-hello-world.yml --syntax-check

# Check
ansible-playbook -i inventory.txt  playbooks/simple/basic/basic-hello-world.yml --check

# Execute
ansible-playbook -i inventory.txt playbooks/simple/basic/basic-hello-world.yml
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

* Execute the following command (examples-playbooks/simple/basic/)

```bash
ansible-playbook -i inventory.txt playbooks/simple/basic/basic-print-facts.yml
```





### Ping Playbook

**Example 1 : Pinging Group**

Step to follow:

* Create "ping.yml" file in playbooks

```bash
---
- name: Ping Group 
  hosts: all_targets
  tasks:
  - name: Ping Group
    ping:
```

* Execute the following command (examples-playbooks/simple/ping/)

```bash
ansible-playbook -i inventory.txt playbooks/simple/ping/ping.yml
```





### Reboot Playbook

**Example 1 : Reboot and wait hosts**

Step to follow:

* Create "rebot-wait.yml" file in playbooks

```bash
---
- name: Reboot and wait
  hosts: all_targets
  tasks:

  - name: Rebooting
    shell: sleep 2 && reboot
    async: 1
    poll: 0

  - name: Waiting for rebooting
    wait_for_connection:
      delay: 15
      sleep: 10
      timeout: 300 

  - debug:
        msg: "{{ inventory_hostname }} is up and running"
```

* Execute the following command (examples-playbooks/simple/reboot/)

```bash
ansible-playbook -i inventory.txt playbooks/simple/reboot/rebot-wait.yml
```





### File Playbook

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

* Execute the following command (examples-playbooks/simple/file/)

```bash
ansible-playbook -i inventory.txt playbooks/simple/file/file-create-empty-file.yml
```

* Verify

```bash
ssh ansible-target-1

ls

exit
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

* Execute the following command (examples-playbooks/simple/file)

```bash
ansible-playbook -i inventory.txt playbooks/simple/file/file-create-directory.yml
```

* Verify

```bash
ssh ansible-target-1

ls

exit
```





### User Playbook

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

* Execute the following command (examples-playbooks/simple/user/)

```bash
ansible-playbook -i inventory.txt playbooks/simple/user/user-create-test-user.yml
```

Verify 

```bash
ssh ansible-target-1

cat /etc/passwd

su test

exit
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

* Execute the following command (examples-playbooks/simple/user)

```bash
ansible-playbook -i inventory.txt playbooks/simple/user/user-delete-test-user.yml
```





### Replace Playbook

**Example 1 : Replace Strings user**

Step to follow:

* Create "replace-all-instances-string.yml" file in playbooks

```bash
---
- name: Replace all instances of String
  hosts: all_targets
  become: true
  tasks:
  - name: Copy content to a file
    copy:
      content: "Hello World!\n" 
      dest: /home/ansible/result.txt 
      remote_src: yes
  - name: Replace all instances of a string
    replace: 
      path: /home/ansible/result.txt 
      regexp: 'World'
      replace: 'Test'
  - name: Ensure SELinux is set to enforcing mode
    lineinfile:
      path: /home/ansible/result.txt 
      regexp: 'Test'
      line: 'Test Updated'
```

remove : delete home directory
force : delete all files 

* Execute the following command (examples-playbooks/simple/)

```bash
ansible-playbook -i inventory.txt playbooks/simple/replace-all-instances-string.yml
```

* Verify

```bash
ssh ansible-target-1

cat result.txt

exit
```




### Archive Playbook

**Example 1 : Zip file**

Step to follow:

* Create "archive-create-zip.yml" file in playbooks

```bash
---
- name: Create Zip
  hosts: all_targets
  tasks:
  - name: Ansible zip directory home 'ansible'
    archive:
      path:
      - /home/ansible
      dest: /home/ansible/example.zip
      format: zip
```

* Execute the following command (examples-playbooks/simple/)

```bash
ansible-playbook -i inventory.txt playbooks/simple/archive-create-zip.yml
```

* Verify

```bash
ssh ansible-target-1

ls

exit
```





### Manager Software Package Module (yum for CentOs) / Service Module

**Example 1 : Install vim and git (case 1)**

Step to follow:

* Create "yum-install-1.yml" file in playbooks

```bash
---
- name: Install Package 1
  hosts: all_targets
  become: true
  tasks:
  - name: Install Package 1
    yum: 
      name: vim,git 
      state: latest
```

* Execute the following command (examples-playbooks/simple/yum/)

```bash
ansible-playbook -i inventory.txt playbooks/simple/yum/yum-install-1.yml
```

* Verify

```bash
ssh ansible-target-1

git

exit
```


**Example 2 : Install vim and git (case 2)**

Step to follow:

* Create "yum-install-2.yml" file in playbooks

```bash
---
- name: Install Package 2
  hosts: all_targets
  become: true
  tasks:
  - name: Install Package 2
    yum: 
      name: 
        - vim
        - git 
      state: latest
```

* Execute the following command (examples-playbooks/simple/yum/)

```bash
ansible-playbook -i inventory.txt playbooks/simple/yum/yum-install-2.yml
```

* Verify

```bash
ssh ansible-target-1

git

exit
```


**Example 3 : Install Common Dependencies**

Step to follow:

* Create "yum-install-common-dependencies.yml" file in playbooks

```bash
---
- name: Install Common Dependencies
  hosts: all_targets
  become: true
  tasks:
  - name: Install Common Dependdencies
    yum: 
      name: 
        - libselinux-python
        - libsemanage-python
        - firewalld
      state: latest
```

* Execute the following command (examples-playbooks/simple/yum/)

```bash
ansible-playbook -i inventory.txt playbooks/simple/yum/yum-install-common-dependencies.yml
```

* Verify

```bash
ssh ansible-target-1

python3

exit
```


**Example 4 : Install & Start httpd**

Step to follow:

* Create "yum-install-start-httpd.yml" file in playbooks

```bash
---
- name: Install Package httpd
  hosts: all_targets
  become: true
  tasks:
  - name: Install Package httpd
    yum: name=httpd state=present
  - name: Start httpd service
    service: name=httpd state=started
```

* Execute the following command (examples-playbooks/simple/)

```bash
ansible-playbook -i inventory.txt playbooks/simple/yum-install.yml
```





## Complex

### Install JRE

Step to follow:

* Create "install-jre.yml" file in playbooks

```bash
---
- name: Install JRE
  hosts: all_targets
  become: true
  vars:
    JRE_VERSION: java-1.8.0-openjdk
  tasks:
  - name: Install OpenJDK Java JRE
    yum:
      name: "{{ JRE_VERSION }}"
      state: present
```

* Execute the following command (examples-playbooks/complex/)

```bash
ansible-playbook -i inventory.txt  playbooks/complex/install-jre.yml
```

### Install Maven

Step to follow:

* Create "install-maven.yml" file in playbooks

```bash
---
- name: Install Maven
  hosts: all_targets
  become: true
  vars:
    MAVEN_MAJOR: "3"
    MAVEN_VERSION: "3.6.3"
    MAVEN_DOWNLOAD_URL: "http://www.apache.org/dist/maven/maven-{{ MAVEN_MAJOR }}/{{ MAVEN_VERSION }}/binaries/apache-maven-{{ MAVEN_VERSION }}-bin.tar.gz"
    MAVEN_HOME: "/opt"
    MAVEN_ENV_FILE: "/etc/profile.d/maven.sh"
  tasks:
  
    - name: Check If Maven is already installed
      shell: "mvn -version | grep -w 'Apache Maven' | awk '{print $3}'"
      register: maven_version_installed
  
    - name: Print Maven Version Installed
      debug: "msg={{ maven_version_installed.stdout }}"
    
    # No install
    - block:
    
      - name: Download and Unarchive maven
        unarchive:
          src: "{{ MAVEN_DOWNLOAD_URL }}"
          dest: "{{MAVEN_HOME}}"
          copy: no

      - name: Create maven symlink to /usr/bin
        file:
          src: "{{ MAVEN_HOME }}/apache-maven-{{ MAVEN_VERSION }}/bin/mvn"
          dest: /usr/bin/mvn
          state: link

      - name: Configure maven and its environment variables
        lineinfile:
          dest: "{{MAVEN_ENV_FILE}}"
          line: "{{ item.line }}"
          create: yes
          state: present
        with_items:
        - { line: 'M2_HOME={{MAVEN_HOME}}/apache-maven-{{MAVEN_VERSION}}' }
        - { line: 'PATH=$PATH:$M2_HOME/bin' }

      - name: Exports/Run maven env file for make M2_HOME available globally
        shell: "source {{MAVEN_ENV_FILE}}"
      
      when: maven_version_installed.stdout == ""
```

* Execute the following command (examples-playbooks/complex/)

```bash
ansible-playbook -i inventory.txt  playbooks/complex/install-maven.yml
```

Verify

```bash
ssh ansible-target-1

mvn

echo $M2_HOME

exit
```









## Authors

* **Víctor Madrid**