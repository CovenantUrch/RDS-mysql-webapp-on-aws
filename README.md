<h1>☁️ Web App + Amazon RDS MySQL Deployment on AWS</h1>

This project sets up a simple web application that connects to a MySQL database hosted on Amazon RDS. All resources are created inside a secure Virtual Private Cloud (VPC), with proper network isolation between the web app and database.

---
At the end of this lab, your architecture will look like the following example:
 <br/>
<img src="creating rds database.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
---
<h2>✅ What You’ll Build</h2>

- A secure **VPC** with public and private subnets
- A **MySQL RDS database** inside the private subnet
- A **web application** hosted on **Amazon EC2**
- A working connection between the EC2 and RDS instance

---

<h2>📦 AWS Services Used</h2>

| Service          | Purpose                           |
|------------------|-----------------------------------|
| VPC              | Network isolation & subnets       |
| RDS (MySQL)      | Managed relational database       |
| EC2              | Host the web application          |
| Security Groups  | Control access between resources  |
| IAM (optional)   | Role-based access to Secrets Manager |

---

<h2>🧰 Technologies</h2>

- **MySQL** database engine
- **PHP** or **Node.js** for the app (your choice)
- **Apache** or **Nginx** web server
- **Amazon Linux / Ubuntu** EC2 instance

<h2> 🛠️ Project Setup Instructions</h2>

<h4>✅1. Create VPC with:</h4>
- 2 public subnets
- 2 private subnets
- 1 internet gateway
- Route tables to link everything

<h4>✅2. Launch RDS:</h4>
- At the top of the AWS Management Console, in the search box, enter and select RDS
- Choose Create database.
- Under Engine options, select MySQL.
- Set the templates and availability and durability options:

Under the Templates section, select  Dev/Test.

Under the Availability and durability section, select   Single DB instance 
- Under the Settings section, configure these options:

DB instance identifier: inventory-db

Master username: admin
- Under Credentials management, choose Self managed and configure as follows:

Master password: lab-password

Confirm master password: lab-password
- Under the Instance configuration section, configure these options:

Select Burstable classes (includes t classes).

Select db.t3.micro
- In the Storage section next

For Storage type choose General Purpose SSD (gp2) from the Dropdown menu.

For Allocated storage  enter 20.
- Expand Storage autoscaling 

Clear or Deselect Enable storage autoscaling.
- Under the Connectivity section, configure these options: 

Virtual Private Cloud (VPC): Choose the VPC you created in the first step

DB subnet group: Keep the default selection
- Expand the Additional configuration panel, then configure these settings:

Initial database name: inventory
- Choose Create database (at the bottom of the page).

<h4>✅3. Launch EC2 instance:</h4>
- In **public subnet**
- Allow HTTP/SSH traffic
- Install web server + language runtime
- Place EC2 in the same VPC and region as your RDS

<h4>✅4. Create Web App:</h4>
```php
<?php
$conn = new mysqli("your-db-endpoint", "admin", "lab-password", "inventory-db");
if ($conn->connect_error) {
  die("Connection failed: " . $conn->connect_error);
}
echo "✅ Connected successfully to RDS!";
?>
Replace with your actual RDS endpoint and credentials.

<h4>✅5. Test:</h4>
Visit the EC2 Public IP in your browser

You should see "✅ Connected successfully to RDS!"

<h3>🔒 Security Notes</h3>
EC2 and RDS must be in the same VPC

RDS security group must allow access from EC2

Use Secrets Manager for production secrets

<h1>🙋 Author</h1>
Covenant Urch
AWS Cloud Builder | Lagos, Nigeria
