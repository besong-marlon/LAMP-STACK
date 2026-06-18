## WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS

### **Introduction**:

The LAMP stack is a popular open-source web development platform that consists of four main components: Linux, Apache, MySQL, and PHP (Perl or Python). This documentation outlines the setup, configuration, and usage of the LAMP stack.

#### **Step 0 – Preparing prerequisites**

1. Created an EC Instance of t3.micro type and Ubuntu 24.04 LTS (HVM) and was launched in us-east1 AWS region

![creating_EC2_instanace](./images/creating_EC2_instanace-2.png)2. Created SSH Key pair named lamp-ec2-key to access instance on port 22  
![creatingEC2_key](./images/creatingEC2_key-2.png)

1. The following security group were configured:

- Allow traffic on port 80 (HTTP) with source from anywhere on the internet
- Allow traffic on port 443 (HTTPS) with source from anywhere on the internet
- Allow traffic on port 22 (SSH) with source from any IP address. This is opened by default  
  ![adding_securityGroups](./images/adding_securityGroups.png)

1. The default VPC and Subnet was used for network configurations
   ![showing_network_config](./images/showing_network_config.png)

1.
