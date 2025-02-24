# Cloud Overview

## Lecture Notes: Cloud Concepts Overview

### Topics

* introduction to cloud computing
* advantages of cloud computing
* introduction to Amazon Web Services
* AWS Cloud Adoption Framework

### Introduction to Cloud Computing

* cloud computing is the on-demand delivery of compute power, database, storage, applications, and other IT resources via the internet with pay-as-you-go pricing
* infrastructure as software
  * cloud computing enables you to stop thinking of your infrastructure as hardware, and instead think of (and use) it as software
* traditional computing model
  * infrastructure as hardware
  * hardware solutions:
    * require space, staff, physical security, planning, capital expenditure
    * have a long hardware procurement cycle
    * require you to provision capacity by guessing theoretical maximum peaks
* cloud computing model
  * infrastructure as software
    * software solutions:
      * are flexible
      * can change more quickly, easily, and cost-effectively than hardware solutions
      * eliminate the undifferentiated heavy-lifting tasks
* cloud service models (less control over IT resources as you move down the list)
  * infrastructure as a service
  * platform as a service
  * software as a service
* cloud computing deployment models
  * cloud
  * hybrid
  * on-premises (private cloud)
* key takeaways
  * cloud computing is the on-demand delivery of IT resources via the internet with pay-as-you-go pricing
  * cloud computing enables you to think of (and use) your infrastructure as software
  * three cloud service models: infrastructure as a service, platform as a service, software as a service
  * three cloud deployment models: cloud, hybrid, on-premises
  * almost anything you can implement with traditional IT can also be implemented as an AWS cloud computing service

### Advantages of Cloud Computing

* trade capital expense for variable expense
  * data center investment based on forecast vs paying only for the amount you consume
* massive economies of scale
  * because of aggregate usage from all customers, AWS can achieve higher economies of scale and pass savings on to customers
* stop guessing capacity
  * scaling on demand
* increase speed and agility
  * minutes between wanting resources and having resources
* stop spending money on running and maintaining data centers
* go global in minutes

### Introduction to Amazon Web Services

* a web service is any piece of software that makes itself available over the internet and uses a standardized format (ex. XML or JSON) for the request and the response of an application programming interface (API) interaction
* what is AWS?
  * a secure cloud platform that provides a broad set of global cloud-based products
  * provides you with on-demand access to compute, storage, network, database, and other IT resources and management tools
  * offers flexibility
  * pay only for the individual services you need, for as long as you use them
  * services work together like building blocks
* how to interact with AWS
  * AWS management console
    * easy-to-use graphical interface
  * command line interface
    * access to services by discrete commands or scripts
  * software development kits
    * access services directly from your code

### The AWS Cloud Adoption Framework

* provides guidance and best practices to help organizations build a comprehensive approach to cloud computing across the organization and throughout the IT lifecycle to accelerate successful cloud adoption
* organized into six perspectives
  * each perspective consists of sets of capabilities
* core perspectives:
  * business
  * people
  * governance
  * platform
  * security
  * operations
* business perspective
  * must ensure that IT is aligned with business needs and that IT investments can be traced to demonstrable business results
  * perspective capabilities:
    * IT finance
    * IT strategy
    * benefits realization
    * business risk management
* people perspective
  * must prioritize training, staffing, and organizational changes to build an agile organization
  * perspective capabilities:
    * resource management
    * incentive management
    * career management
    * training management
    * organizational change management
* governance perspective
  * must ensure that skills and processes align IT strategies and goals with business strategies and goals so the organization can maximize the business value of its IT investment and minimize business risks
  * perspective capabilities
    * portfolio management
    * program and project management
    * business performance measurement
    * license management
* platform perspective
  * must understand and communicate the nature of IT systems and their relationships
  * must be able to describe the architecture of the target state environment in detail
  * perspective capabilities:
    * compute provisioning
    * network provisioning
    * storage provisioning
    * database provisioning
    * systems and solution architecture
    * application development
* security perspective
  * must ensure that the organization meets its security objectives
  * perspective capabilities:
    * identity and access management
    * detective control
    * infrastructure security
    * data protection
    * incident response
* operations perspective
  * align with and support the operations of the business and define how day-to-day, quarter-to-quarter, and year-to-year business will be conducted
  * perspective capabilities:
    * service monitoring
    * application performance monitoring
    * resource inventory
    * release management/change management
    * reporting and analytics
    * business continuity/disaster recovery
    * IT service catalog
* key takeaways
  * cloud adoption is not instantaneous for most organizations and requires a thoughtful, deliberate strategy and alignment across the whole organization
  * the AWS CAF was created to help organizations develop efficient and effective plans for their cloud adoption journey
  * the AWS CAF organizes guidance into six areas of focus, called perspectives
  * perspectives consist of sets of business or technology capabilities that are the responsibility of key stakeholders

## Lab Notes: AWS Sandbox

* AWS Academy Canvas -> AWS Academy Cloud Foundations -> Modules -> Sandbox Environment -> Start Lab
  * can run commands in the console
* AWS -> opens the AWS console
* in console, search for EC2 -> select Dashboard -> Instances -> Launch instances -> name, Amazon Linux, instance type t2.micro free tier, key pair vockey, allow SSH traffic from anywhere -> Launch Instance
  * can return to Instances and click on new instance to see public IP
* in sandbox, Details -> Show -> Download PEM
* open Powershell

```
cd Downloads
ssh -i labsuser.pem ec2-user@[public IP]
```

* end lab when done

## Lab Notes: AWS Learner Lab

* AWS Academy Canvas -> AWS Academy Learner Lab -> Modules -> Launch AWS Academy Learner Lab -> Start Lab -> click on AWS icon when it turns green
* in the console, search for EC2 -> under Network and Security, Key Pairs -> Create key pair -> name, RSA, .pem for SSH (not Putty) -> Create key pair
  * private key is automatically downloaded by browser, save somewhere safe
  * may have to set permissions to 400 to use (especially on a Linux system)
* under Network and Security, Security Groups -> Create security group -> make sure area is set to United states (N. Virginia) -> name, description, leave VPC default
* inbound rules:
  * HTTP from anywhere
  * HTTPS from anywhere
  * SSH from My IP
* create security group
* end lab when done

## Lab Notes: Wordpress on AWS Instance

* instance should be Amazon Linux 2 free tier (not just Amazon Linux)

```
# Initial Setup
ssh -i [key].pem ec2-user@[public IP]
sudo yum update -y
sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2
sudo yum install -y httpd mariadb-server
sudo systemctl start httpd
sudo systemctl enable httpd
sudo usermod -a -G apache ec2-user
exit
ssh -i [key].pem ec2-user@[public IP]
sudo chown -R ec2-user:apache /var/www
sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;
find /var/www -type f -exec sudo chmod 0664 {} \;
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
# MariaDB
sudo systemctl start mariadb
sudo mysql_secure_installation
sudo systemctl enable mariadb
# PHP
sudo yum install php-mbstring -y
sudo systemctl restart httpd
sudo systemctl restart php-fpm
cd /var/www/html
wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.gz
mkdir phpMyAdmin && tar -xvzf phpMyAdmin-latest-all-languages.tar.gz -C phpMyAdmin --strip-components 1
rm phpMyAdmin-latest-all-languages.tar.gz
# Installing Wordpress
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
mysql -u root -p
CREATE USER 'wordpress-user'@'localhost' IDENTIFIED BY '[password]';
CREATE DATABASE `wordpress-db`;
GRANT ALL PRIVILEGES ON `wordpress-db`.* TO "wordpress-user"@"localhost";
FLUSH PRIVILEGES;
exit
cp wordpress/wp-config-sample.php wordpress/wp-config.php
nano wordpress/wp-config.php
# define('DB_NAME', 'wordpress-db');
# define('DB_USER', 'wordpress-user');
# define('DB_PASSWORD', '[password]');
# Use link below to paste values into Authentication Unique Keys and Salts section
cp -r wordpress/* /var/www/html/
sudo nano /etc/httpd/conf/httpd.conf
# go to Directory /var/www/html section and change AllowOverride to All
sudo yum install php-gd
sudo chown -R apache /var/www
sudo chgrp -R apache /var/www
sudo chmod 2775 /var/www 
find /var/www -type d -exec sudo chmod 2775 {} \;
find /var/www -type f -exec sudo chmod 0664 {} \;
sudo systemctl restart httpd
sudo systemctl enable httpd && sudo systemctl enable mariadb
sudo systemctl status mariadb
sudo systemctl status httpd
```

* can now go to the site and finish the Wordpress installation

{% embed url="https://api.wordpress.org/secret-key/1.1/salt/" %}
