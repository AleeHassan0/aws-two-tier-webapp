

#Web Server Setup (Apache + PHP EC2)

This document describes all commands used to configure the Web Server EC2 instance for the AWS Two-Tier Architecture project.

------------------------------------------------------------

Connect to EC2 via SSH

ssh -i aws-capstone-key.pem ec2-user@<public-ip>

------------------------------------------------------------

Install Apache (HTTPD)

sudo dnf install httpd -y

------------------------------------------------------------

Start and Enable Apache Service

sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl status httpd

------------------------------------------------------------

Test Apache in Browser

Open in browser:

http://<public-ip>

Apache default page should load successfully.

------------------------------------------------------------

Install PHP and MySQL Driver

sudo dnf install php php-mysqlnd -y

------------------------------------------------------------

Restart Apache After PHP Installation

sudo systemctl restart httpd

Check PHP version:

php -v

------------------------------------------------------------

Navigate to Web Directory

cd /var/www/html

------------------------------------------------------------

Remove Default Apache Page (Optional)

sudo rm index.html

------------------------------------------------------------

Create Application File

sudo nano index.php

(Paste final Guestbook PHP application code here)

------------------------------------------------------------

Configure Database Connection Inside index.php

Set the following values inside the PHP file:

$servername = "DB_PRIVATE_IP";
$username = "Hassan";
$password = "Hassan@123";
$dbname = "myDatabase";

Replace DB_PRIVATE_IP with the private IP of the Database EC2 instance.

------------------------------------------------------------

Update Database Security Group (AWS Console Step)

• Remove My IP from Port 3306  
• Add Source: web-server-sg  
• Ensure Port 80 (HTTP) is open to 0.0.0.0/0  
• Ensure Port 22 (SSH) is restricted to My IP  

------------------------------------------------------------

est Full Application

Open in browser:

http://<public-ip>

• Guestbook page should load  
• Submit form  
• Data should be inserted into MySQL database  
• Messages should display on the page  

------------------------------------------------------------

Result

Web Server EC2 successfully configured with:
• Apache installed and running
• PHP installed
• Application deployed
• Connected securely to Database EC2 via private IP
• Public access allowed only on Port 80
• SSH restricted to trusted IP

