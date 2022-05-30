# Installation

## ubuntu

<https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04>

### Installing MySQL

```shell
sudo apt update
sudo apt install mysql-server
sudo systemctl start mysql.service
```

### Configuring MySQL

```shell
$ sudo mysql_secure_installation
Output
Securing the MySQL server deployment.

Connecting to MySQL using a blank password.

VALIDATE PASSWORD COMPONENT can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD component?

Press y|Y for Yes, any other key for No: Y

There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG:
 2
Output
Please set the password for root here.


New password:

Re-enter new password:
```
