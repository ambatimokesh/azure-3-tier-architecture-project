3-Tier Architecture Deployment in Microsoft Azure

Project Overview

This project demonstrates the implementation of a 3-Tier Architecture in Microsoft Azure using Virtual Machines, Virtual Networks, and Network Security Groups.

The architecture consists of three layers:
Web Layer – Handles client requests using Nginx
Application Layer – Processes application logic using Apache Tomcat
Database Layer – Stores data using MySQL
This design improves security, scalability, and maintainability.


![3 tire ](https://github.com/user-attachments/assets/769a829f-1a73-4f6d-8d21-04691e0555ce)




Cloud Platform : Microsoft Azure

Architecture Components

WEB SERVER:

Nginx
Public access via HTTP (Port 80)

APPLICATION SERVER:

Apache Tomcat
Communicates with Web Server

DATABASE SERVER:

MySQL
Accessible only from App Server

Network Architecture

Virtual Network contains three subnets

Web Subnet
App Subnet
DB Subnet
Security rules allow communication only between required servers.

Network Security Rules

WEB SERVER:
Allowed Ports
  22 (SSH)
  80 (HTTP)

APPLICATION SERVER:
Allowed Ports
   22 (SSH)
   8080 (Tomcat)

DATABASE SERVER:
Allowed Ports
  22 (SSH)
  3306 (MySQL)

Software Installation
Install Nginx (Web Server)  
sudo apt update
sudo apt install nginx -y

Install Tomcat (Application Server)

Ssh username@appserver_private_ip 
Check: hostname 
Bash: 
sudo apt update 
sudo apt install openjdk-17-jdk -y 
java -version 
cd /opt 
sudo wget https://archive.apache.org/dist/tomcat/tomcat-11/v11.0.18/bin/apache-tomcat
11.0.18.tar.gz 
sudo tar -xvzf apache-tomcat-11.0.18.tar.gz 
sudo mv apache-tomcat-11.0.18 tomcat 
ls /opt 
cd /opt/tomcat/bin 
sudo ./startup.sh 
sudo ss -tulnp | grep 8080 
0.0.0.0:8080

Install MySQL (Database Server)

ssh username@dbserver_private_ip 
Check: hostname 
Bash: 
sudo apt update 
sudo apt install mysql-server -y 
sudo systemctl status mysql 
sudo mysql_secure_installation 
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf 
Find       
: bind-address = 127.0.0.1 
Change To : bind-address = 0.0.0.0 
sudo systemctl restart mysql 
sudo mysql -u root -p 
INSIDE MYSQL: 
CREATE DATABASE appdb; 
CREATE USER 'appuser'@'%' IDENTIFIED BY 'password123'; 
GRANT ALL PRIVILEGES ON appdb.* TO 'appuser'@'%'; 
FLUSH PRIVILEGES; 
EXIT; 
TEST FROM APP SERVER : 
mysql -h db_private_ip -u appuser -p 
After installation, tested database connectivity using: 
telnet 3306

Connectivity Testing

Test communication using Telnet
telnet <APP-SERVER-IP> 8080
telnet <DB-SERVER-IP> 3306
Successful connection confirms network communication between layers.



Project Architecture

Web Server → App Server → Database Server

Client → Nginx → Tomcat → MySQL

Key Learnings

Cloud Infrastructure Deployment
Network Security Configuration
Linux Server Management
Multi-tier Application Architecture
Azure Networking Concepts

Author
AMBATI MOKESH REDDY
BCA Graduate
Cloud & DevOps Enthusiast
