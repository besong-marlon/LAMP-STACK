# WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS

## Introduction:

The LAMP stack is a popular open-source web development platform that consist of four main components: Linux, Apache, MySQL and PHP (Perl or Python). This documentation outlines the setup, configuration, and usage of the LAMP stack.

### ++Step 0 - Preparing prerequisites++

**1- Created an EC2 instance of t3.micro type which happens to be a free tier and Ubuntu 24.04 LTS (HVM) and was launched in us-east1 AWS region.**

![creating_EC2_instanace](./images/creating_EC2_instanace.png)

**2- Created SSh key pair named lamp-ec2-key to access instance on port 22**

![creatingEC2_key](./images/creatingEC2_key.png)

**3- The following security grops were congigured:**

- Allow traffic on port 80 (HTTP) with source from anywhere on the internet
- Allow traffic on port 443 (HTTPS) with source from anywhere on the internet
- Allow traffic on port 22 (SSH) with source from any IP address. This is opened by default.  
![adding_securityGroups](./images/adding_securityGroups.png)

**4- The default VPC and subnet was used for network configurations**

![showing_network_config](./images/showing_network_config.png)

**5- The SSH protocol was used to establish connectivity to the EC2 instance by using the following command on**

```bash
ssh -i lamp-ec2-key.pem ubuntu@54.234.122.249
```

![connectingToEC2By_ssh](./images/connectingToEC2By_ssh.png)

### Step 1 - Installing Apache and Update the firewall

**1- Updating and upgrading list of packages in package manager**

```bash
sudo apt update
sudo apt upgrade -y
```

![updatingServer](./images/updatingServer.png)![upgradingServer](./images/upgradingServer.png)

**2- Run apache2 package**

```bash
sudo apt install apache -y
```

![installingApache2](./images/installingApache2.png)

**3- Enable and verify that apache is running as a service on the OS**

```bash
sudo systemctl enable apache2
sudo systemctl status apache2
```

![enablingAndVerifyingApache](./images/enablingAndVerifyingApache.png)

**4- The server is running and can be accessed locally in the ubuntu shell by running the command below:**

```bash
curl http://localhost:80

OR

curl http://127.0.0.1:80
```

![server_is_running](./images/server_is_running.png)

**5- Test with the public IP address if the Apache HTTP server can respond to request from the internet using the url on a browser**

```bash
http://54.234.122.249:80
```

![Apache2_defaultPage](./images/Apache2_defaultPage.png)

This shows that the web server is corectly installed and it is accessible through the firewall.

### ++Step 2 - Installing MySQL++

**1- Install a relational database (RDB)**

MySQL was installed in this project. it is a popular relational database management system used whithin PHP environment and other frameworks.

```bash
sudo apt installl mysql-server
```

![installingMySQL](./images/installingMySQL.png)When prompted, installation was confirmed by typing Y and ENTER.

**2- Enable and verify that mysql is running with the commands below**

```bash
sudo systemctl enable --now mysql
sudo systemctl status mysql
```

![enabling_and_verifyingMySQL](./images/enabling_and_verifyingMySQL.png)

**3- Log into mysql console**

```bash
sudo mysql
```

This connects the MySQL server as the administrative database user root infered by the usef sudo when running the command.

**4- Set a password for root user mysql_native_password as a default authentication method her, the user's password was defined as "Password.1"**

```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
```

![loggingI_toMySQl_console](./images/loggingI_toMySQl_console.png)Exit the MySQL shell

```bash
exit
```

**5- Run an interactive scrip to secure MySQL**

The security script comes pre-installed with mysql. This script removes some insecure settings and lock down access to the database system

```bash
sudo mysql_secure_installation
```

ggc![mysql_secure_installation](./images/mysql_secure_installation.png)

Regardless of whether you chose to set up the `VALIDATE PASSWORD PLUGIN`, your server will next ask you to select and confirm a password for the MySQL **root** user.

**6- After changing root user password, loginto MySQL console.**

A command prompt for password was noticed after running the command below.

```bash
sudo mysql -p
```

![logInto_mysql_afterPassword_change](./images/logInto_mysql_afterPassword_change.png)Exit MySQL shell

```bash
exit
```

### ++Step 3 - Installing PHP++

**1- **You have Apache installed to serve your content and MySQL installed to store and manage your data. PHP is the component of our setup that will process code to display dynamic content to the end user.

The following were installed:

- Php package
- php-mysql, a php module that allows PHP to communicate with MySQL-based databases
- libapache2-mod-php, to anable Apache to handle PHP file.

```bash
sudo apt install php libapache2-mod-php php-mysql
```

![installing_php_packages](./images/installing_php_packages.png)

The following command to confirm PHp version

```bash
php -v
```

![php_version](./images/php_version.png)

At this point, your LAMP stack is completely installed and fully operational.

To test your setup with a PHP script, it’s best to set up a proper Apache Vitual Host to hold your website’s files and folders. Virtual host allows you to have multiple websites located on a single machine and users of the websites will not even notice it.

### ++Step4 - Create a virtual host for the website using Apache++

**1-  The default directory serving the apache default page is /var/www/html. Create your doucment directory next to the default one.**

Create the directory for projectlamp using "mkdir" command

```bash
sudo mkdir /var/www/projectlamp
```

Assign the directory ownership with $USER environment variable which references the current system user.

```bash
sudo chown -R $USER:$USER /var/www/projectlamp
```

![creatingProject_directory](./images/creatingProject_directory.png)

**2- Create and open a new configuration file in apache's "sites-available" directory using vim.**

```bash
sudo vim /etc/apache2/sites-available/projectlamp.conf
```

Past the bare-bones configuration below:

```bash
<VirtualHost *:80>
  ServerName projectlamp
  ServerAlias www.projectlamp
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/projectlamp
  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

![bareBone_config](./images/bareBone_config.png)

3- Show the new file sites-available

```bash
sudo ls /etc/apache2/sites-available
```

```bash
Output:
000-default.conf default-ssl.conf projectlamp.conf
```

![sitesAvailable](./images/sitesAvailable.png)

With the VirtualHost configuration, Apache will serve projectlamp using /var/www/projectlamp as its web root directory.

**4- Enable the new virtual host**

```bash
sudo a2ensite projectlamp
```

![enabling-new-virtualHost](./images/enabling-new-virtualHost.png)

**5- Disable Apache's default website.**

This is because Apache’s default configuration will overwrite the virtual host if not disabled. This is required if a custom domain is not being used.

```bash
sudo a2dissite 000-default
```

![disabling_defaultApacheSite](./images/disabling_defaultApacheSite.png)

**6- Ensure the configuration does not contain syntax error**

**The command below was used:**

```bash
sudo apache2ctl configtest
```
