# install-virtualbox

This document shows the description of how to install Ansible in a simple way





## Technological Stack

* [Virtual Box](https://www.virtualbox.org/) - Virtualization product
* [CentOs](https://www.centos.org/) - Linux distribution (Fork GNU/Linux Red Hat Enterprise Linux RHE)





## Prerequisites

>**Important**
> 
>For Windows, you may be required to enable virtualization technology from the BIOS





## Installation

>**Important**
>
>A control node or control machine is required to manage the other machines
>
>That control node should be Linux since Windows machines do NOT support it
>Requires you to have Python 2/3 installed (Currently 3)
>
>Remember that the control machine must have access to all other

Step to follow:

* Note : The distribution of CentOs will be used
* It is required to enable the EPEL repo : **sudo yum install epel-release**
* Required to install ansible : **sudo yum install ansible**
* Verify the installation : **ansible -version**


### Configuration

Global configuration file (default) : **/etc/ansible/ansible.cfg**

To modify it
sudo vi /etc/ansible/ansible.cfg
Enable the "inventory" file parameter

Global inventory file (default) : **/etc/ansible/hosts**

To modify it
sudo vi /etc/ansible/hosts






## Testing

N/A





## Deploy

N/A





## Use

N/A





## Versioning

**Note :** [SemVer](http://semver.org/) is used for the versioning.
To see the available versions access the repository tags





## Authors

* **Víctor Madrid** 