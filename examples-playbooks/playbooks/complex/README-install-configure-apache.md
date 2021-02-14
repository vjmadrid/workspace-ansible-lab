# install-configure-apache

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
    * Dependencies : httpd y firewalld
    * sudo yum install XXX



## Install & Configure Apache

* Start & Enable Services
    * sudo service httpd start
    * sudo systemctl enable httpd
    * sudo service firewalld start
    * sudo systemctl enable firewalld
* Change Apache Configuration Port -> replace port 80 to 8090 
    * /etc/httpd/conf/httpd.conf
* Restart Apache Service
    * sudo service httpd start
* Add firewall Rule for Apache


Apache
	 * install httpd
	 	sudo yum install -y httpd php php-mysql

	 * configure httpd
	 	sudo firewall-cmd --permanent --zone=public --add-port=80/tcp
	 	sudo firewall-cmd --reload
	 * configure firewall
	 	sudo vi /etc/httpd/conf/httpd.conf
	 * start httpd
	 	sudo service httpd start


## Prepare Database for MariaDB

* Create "acmedb" Database
* Create user
* Create grants

```bash
mysql
MariaDB > CREATE DATABASE acmedb;
MariaDB > CREATE USER 'acmeuser'@'localhost' IDENTIFIED BY 'acmepassword'
MariaDB > GRANT ALL PRIVILEGES ON *.* TO 'acmeuser'@'localhost';
FLUSH PRIVILEGES;
mysql Z dbxxx.sql
```
     	
     * load data

