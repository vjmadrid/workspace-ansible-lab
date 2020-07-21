# install-vdi-centos7

This document shows the description of how to install a CentOs7 VDI on Virtual Box in a simple way





## Technological Stack

* [Virtual Box](https://www.virtualbox.org/) - Virtualization product
* [CentOs](https://www.centos.org/) - Linux distribution (Fork GNU/Linux Red Hat Enterprise Linux RHE)





## Installation


### Download CentOs7 VDI

Step to follow:

* Access to [https://www.osboxes.org/](https://www.osboxes.org/)
* Select "CentOs" or Access to [https://www.osboxes.org/centos/](https://www.osboxes.org/centos/)
* Download the latest version of CentOS 7 for Virtualbox -> For example : CentOS 7-1908
* Decompress into a directory
* Verify that a .vdi file exists

**Info Centos7 VDI**

```bash
Username: osboxes
Password: osboxes.org
Root Account Password: osboxes.org
VB Guest Additions & VMware Tools: Not Installed
Keyboard Layout: US (Qwerty)
VMware Compatibility: Version 10+
```



### Create CentOs Template for VirtualBox

Step to follow:

* Click "New"
* Select:
    * name: **centos7-template**
    * type: **Linux**
    * name: **Other Linux (64-bit)**
* Select memory: **2048MB**
* Select hard disk: **"Use an existing virtual hard disk file"** and select the location of the downloaded VDI



### Configure "centos7-template"

Step to follow:

* At the **System** level 
    * Set up processors: **minimum 2**
* At the **Network** level
    * Set **"Bridged Adapter"**





## Testing


### Start "centos7-template" VM

Step to follow:

* Test that it works by starting it up
* Login with the data set in "osboxes
* Execute from the end : ifconfig to verify the assigned IP
    * This means that VM has internet



### External connection "centos7-template" VM

Step to follow:

* Try to enter the machine through that IP from : ssh, mobaxterm, etc.

```bash
ssh osboxes@<IP>
```

* Execute : **shutdown now**





## Deploy

N/A





## Use

N/A





## Versioning

**Note :** [SemVer](http://semver.org/) is used for the versioning.
To see the available versions access the repository tags





## Authors

* **Víctor Madrid** 