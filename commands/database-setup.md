# Database Server Setup (MySQL EC2)

This document describes all commands used to configure the Database EC2 instance for the AWS Two-Tier Architecture project.

------------------------------------------------------------

Connect to EC2 via SSH

ssh -i aws-capstone-key.pem ec2-user@<public-ip>

------------------------------------------------------------

Install MySQL Repository

wget https://dev.mysql.com/get/mysql80-community-release-el9-1.noarch.rpm
sudo dnf install mysql80-community-release-el9-1.noarch.rpm -y

------------------------------------------------------------

Install MySQL Server

sudo dnf install mysql-community-server -y

------------------------------------------------------------

Start and Enable MySQL Service

sudo systemctl start mysqld
sudo systemctl enable mysqld
sudo systemctl status mysqld

------------------------------------------------------------

Retrieve Temporary Root Password

sudo grep 'temporary password' /var/log/mysqld.log

------------------------------------------------------------

Login to MySQL

mysql -u root -p

(Enter temporary password from log file)

------------------------------------------------------------

Change Root Password

ALTER USER 'root'@'localhost' IDENTIFIED BY ‘Hassan@123’;

------------------------------------------------------------

Create Database

CREATE DATABASE myDatabase;
USE myDatabase;

------------------------------------------------------------

Create Guestbook Table

CREATE TABLE guestbook (
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    message TEXT NOT NULL
);

------------------------------------------------------------

Create Database User and Grant Privileges

CREATE USER 'Hassan'@'%' IDENTIFIED BY 'Hassan@123';
GRANT ALL PRIVILEGES ON myDatabase.* TO 'Hassan'@'%';
FLUSH PRIVILEGES;

------------------------------------------------------------

Update Security Group (AWS Console Step)

• Remove My IP from Port 3306  
• Add Source: web-server-sg  
• Keep Port 22 (SSH) restricted to My IP  

------------------------------------------------------------

Result

Database EC2 successfully configured with:
• MySQL installed
• Database created
• Table created
• Dedicated DB user configured
• Port 3306 restricted to Web Server only
