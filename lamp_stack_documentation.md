## WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS

**Introduction**:

The LAMP stack is a popular open-source web development platform that consists of four main components: Linux, Apache, MySQL, and PHP (Perl or Python). This documentation outlines the setup, configuration, and usage of the LAMP stack.

**Step 0 – Preparing prerequisites**

1. Created an EC Instance of t3.micro type and Ubuntu 24.04 LTS (HVM) and was launched in us-east1 AWS region

![1781671817879](image/lamp_stack_documentation/1781671817879.png)

2. Created SSH Key pair named lamp-ec2-key to access instance on port 22

![1781671830269](image/lamp_stack_documentation/1781671830269.png)

3. The following security group were configured:
   - Allow traffic on port 80 (HTTP) with source from anywhere on the internet
   - Allow traffic on port 443 (HTTPS) with source from anywhere on the internet
   - Allow traffic on port 22 (SSH) with source from any IP address. This is opened by default

![1781671854892](image/lamp_stack_documentation/1781671854892.png)

4. The default VPC and Subnet was used for network configurations

![1781671867179](image/lamp_stack_documentation/1781671867179.png)

5. The
