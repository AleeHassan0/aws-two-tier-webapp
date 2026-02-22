#AWS Two-Tier Web Application Deployment

This project demonstrates a secure Two-Tier Architecture deployed on AWS using two EC2 instances.

The application is a dynamic Guestbook built with Apache, PHP, and MySQL, where users can submit and view messages.

---

##Architecture Overview

![Architecture Diagram](architecture/architecture-diagram.png)

This project follows a Two-Tier model:

- Presentation Layer → Web Server EC2
- Data Layer → Database Server EC2

Web Server communicates with Database using private IP for secure internal communication.

---

##Architecture Components

###Web Server EC2
- Amazon Linux 2023
- Apache (httpd)
- PHP
- Publicly accessible via Port 80
- Security Group: web-server-sg
  - Port 22 → My IP
  - Port 80 → 0.0.0.0/0

###Database EC2
- Amazon Linux 2023
- MySQL Server
- Database: myDatabase
- Table: guestbook
- Security Group: db-server-sg
  - Port 22 → My IP
  - Port 3306 → Allowed only from web-server-sg

---

##Security Design

- Database is NOT publicly accessible
- MySQL Port 3306 restricted to Web Server Security Group
- SSH access limited to trusted IP
- Separation of Web and Database improves security and scalability

---

##Technologies Used

- AWS EC2
- Amazon Linux 2023
- Apache (httpd)
- PHP
- MySQL
- Security Groups
- SSH

---

##Project Structure


aws-two-tier-webapp/ │ ├── app/ │ └── index.php │ ├── architecture/ │ ├── architecture.md │ └── architecture-diagram.png │ ├── commands/ │ ├── database-setup.md │ └── webserver-setup.md │ ├── screenshots/ │ ├── db-server/ │ └── web-server/ │ └── README.md

 Project Structure

```
aws-two-tier-webapp/
│
├── app/
│   └── index.php
│
├── architecture/
│   ├── architecture.md
│   └── architecture-diagram.png
│
├── commands/
│   ├── database-setup.md
│   └── webserver-setup.md
│
├── screenshots/
│   ├── db-server/
│   └── web-server/
│
└── README.md
```

---

##Application Features

- User submits name and message
- Data stored in MySQL database
- Messages dynamically retrieved and displayed
- Clean and responsive UI design

---

##Learning Outcomes

- Deploying multiple EC2 instances
- Configuring Security Groups
- Installing and managing Apache & MySQL
- Implementing secure private IP communication
- Designing real-world Two-Tier Architecture

---

##Future Improvements

- Configure HTTPS using SSL (Let's Encrypt)
- Use Amazon RDS instead of MySQL on EC2
- Implement Load Balancer
- Add Auto Scaling
- Deploy with Infrastructure as Code (Terraform)

---

##Author

Ali Hassan  
AWS Two-Tier Architecture Project  
