# add-ansible-user

This document shows the description of how to add a new user for Ansible





## Technological Stack

* [Virtual Box](https://www.virtualbox.org/) - Virtualization product
* [CentOs](https://www.centos.org/) - Linux distribution (Fork GNU/Linux Red Hat Enterprise Linux RHE)





## Prerequisites

* Requires having a centos7 VM configured and tested





## Installation

N/A





## Testing

N/A





## Deploy

N/A





## Use

### Add "ansible" user with Sudoers

>**Important** 
>
>"Add user to sudoers file" - NO Password required
>
>Users and groups with privileges are configured in /etc/sudoers
>
>It would be enough to add the user to this file
>
>Options : Modify the sudoers file or create a new configuration in /etc/sudoers.d
>
>Note : Create "ansible" user with SUDO privileges



Step to follow:

* Log in in each server as root user : ansible-controller, ansible-target-1 and ansible-target-1
* Check if you have access to the /root directory (sign that you are root) : **ls -la /root**
* Add user : **useradd ansible**
* Add password : **passwd ansible** (Set value : changeit2020)
* Edit the file /etc/sudoers : **sudo vi /etc/sudoers** 
    * The file is in "Read Only" format so it will be better modified with : **visudo**
    * Locate the section "## Same thing without a password"
    * Add the entry : ansible ALL=(ALL) NOPASSWD: ALL 
* Change the user "ansible" : **su - ansible** (You should not ask for a password)
* Check if you have access to the /root directory (sign that you are root) : **sudo ls -la /root**






## Versioning

**Note :** [SemVer](http://semver.org/) is used for the versioning.
To see the available versions access the repository tags





## Authors

* **Víctor Madrid** 