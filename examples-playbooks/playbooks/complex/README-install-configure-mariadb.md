# install-configure-mariadb

## Define Inventory

Initial Iventory

```bash
[db_server]
db-server-1 ansible_host=XXX ansible_user=ansible ansible_ssh_pass=ansible

[web_servers]
web-server-1 ansible_host=YYY ansible_user=ansible ansible_ssh_pass=ansible
```

Generate SSH for the user "ansible" in the control machine

```bash
ssh-keygen -f /home/thor/.ssh/ansible 
```

Copy SSH for the user "ansible" in the db-server-1

```bash
ssh-copy-id -i ~/.ssh/ansible ansible@db-server-1 
```

Copy SSH for the user "ansible" in the web-server-1

```bash
ssh-copy-id -i ~/.ssh/ansible ansible@web-server-1
```


```bash
[db_server]
db-server-1 ansible_host=XXX ansible_ssh_private_key_file=~/.ssh/ansible ansible_user=ansible mysql_service=mysqld mysql_port=3306 db_name=acmedb db_user=acmeuser db_password=acmepassword

[web_servers]
web-server-1 ansible_host=YYY ansible_ssh_private_key_file=~/.ssh/ansible ansible_user=ansible httpd_port=80 repository=https://github.com/ZZZ
```



## Prepare Environment for MariaDB

* Identify OS
* Install common dependencies
    * Dependencies : libselinux-python, libsemanage-python and firewalld
    * sudo yum install XXX
* Start mariadb service
    * sudo service firewalld start
    * sudo systemctl enable firewalld



## Install & Configure MariaDB

* Install mariadb package
    * sudo yum install mariadb-server
* Configure mariadb
    * sudo vi /etc/my.cnf
* Start mariadb service
    * sudo service mariadb start
	* sudo systemctl enable mariadb
* Insert firewalld Rule for mariadb
     * sudo firewall-cmd --permanent --zone=public --add-port=3306/tcp
     * sudo firewall-cmd --reload

## Prepare Database for MariaDB

* Create "acmedb" Database
* Create user
* Create grants

```bash
mysql
MariaDB > CREATE DATABASE acmedb;
MariaDB > show databases;
MariaDB > CREATE USER 'acmeuser'@'localhost' IDENTIFIED BY 'acmepassword'
MariaDB > GRANT ALL PRIVILEGES ON *.* TO 'acmeuser'@'localhost';
FLUSH PRIVILEGES;
mysql Z dbxxx.sql
```
     	
     * load data

