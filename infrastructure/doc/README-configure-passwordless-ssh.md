# configure-passwordless-ssh

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

### Activate Access and Authorization for "ansible-control"

Step to follow:

* Edit the /etc/ssh/sshd_config file of the control machine : **sudo vi /etc/ssh/sshd_config**
* Locate and enable : **PasswordAuthentication**
* Locate and enable : **PermitRootLogin**
* Restarting the sshd service : **systemctl restart sshd**



### Generate SSH Key "ansible-controller" with "ansible" user

Step to follow:

* Login "ansible-controller" with user "ansible"
* Execute the command : **ssh-keygen**
    * Fill in the fields as empty


### Generate SSH Key "ansible-target-X" with "ansible" user

Step to follow:

* Login "ansible-target-X" with user "ansible"
* Execute the command : **ssh-keygen**
    * Fill in the fields as empty



### Exchange SSH Key "ansible-controller" with "ansible-target-X"

Step to follow:

* Login "ansible-controller" with user "ansible"
* Execute the command : **ssh-copy-id <IP-TARGET_X>**
* Try direct login with ssh <IP_TARGET_X>



### Exchange SSH Key "ansible-target-X" with "ansible-controller"

Step to follow:

* Login "ansible-target-X" with user "ansible"
* Execute the command : **ssh-copy-id <IP-CONTROLLER>**
* Try direct login with ssh <IP-CONTROLLER>





## Versioning

**Note :** [SemVer](http://semver.org/) is used for the versioning.
To see the available versions access the repository tags





## Authors

* **Víctor Madrid** 