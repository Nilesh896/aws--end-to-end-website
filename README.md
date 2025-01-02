# End-to-End Website Deployment on AWS

## Project Overview
This project demonstrates the deployment of a fully functional website using AWS services.
The application is a Flask-based web interface integrated with a MySQL database on AWS RDS, an S3 bucket for file storage, and an EC2 instance for hosting. 
Route 53 is used to map a custom domain to the EC2 instance.

## System Requirements
### AWS Services
- **Amazon RDS**: Managed MySQL database service.
- **Amazon S3**: Scalable object storage.
- **Amazon EC2**: Virtual server hosting.
- **Amazon Route 53**: DNS and domain name management.

### Software and Tools
- **PuTTY & PuTTYgen**: For SSH access (on Windows).
- **Python 3**: With Flask, PyMySQL, and Boto3.
- **MySQL Client**: For RDS database connectivity.


## Deployment Steps

### 1. Set Up MySQL Database on Amazon RDS
1. Navigate to the RDS console and create a new database.
2. **Engine**: MySQL (Community Edition, 8.0.39).
3. **Instance Identifier**: `employee1`.
4. **Credentials**: Username: `Nilesh`, Password: `<Your Password>`.
5. Enable **Public Accessibility**.
6. **Subnet Group**: Default VPC.
7. Confirm the creation of the database and note the **Endpoint URL**.


### 2. Create an S3 Bucket
1. Navigate to the S3 console and create a new bucket.
2. **Bucket Name**: `nileshbucket58`.
3. **Region**: US East (Ohio).
4. Disable **ACLs** (set all objects to be owned by you).
5. Leave **Public Access Block** enabled for security.
6. Confirm the bucket creation.


### 3. Launch an EC2 Instance
1. Navigate to the EC2 console and launch a new instance.
2. **Instance Name**: `my-web-server`.
3. **AMI**: Ubuntu 20.04 (free-tier eligible).
4. **Key Pair**: Create and download a `.pem` key named `webserver`.
5. Confirm the instance creation and note its **Public IP Address**.


### 4. Establish EC2 Connection
#### On Linux/Mac:
---bash

 ssh -i webserver.pem ubuntu@<EC2_Public_IP>

###On Windows:

1.Convert webserver.pem to webserver.ppk using PuTTYgen.
2.Open PuTTY and configure:
  Host Name: <EC2_Public_IP>.
   Port: 22.
    Auth: Use the .ppk file.
3.Save the session and connect.
####  Deploy Flask Application
1.Install required Python packages
---bash
sudo apt-get update
sudo apt-get install python3 python3-flask python3-pymysql python3-boto3
2.Clone your application repository or transfer your Flask app files to the instance.
3.Run the application:
---bash
sudo python3 EmpApp.py
4.Verify the app is running locally at http://<EC2_Public_IP>.

####  Integrate S3 and RDS
1.Update your Flask app configuration:
  Database Host: employee1.cxsgw06ge1ty.us-east-2.rds.amazonaws.com.
  Bucket Name: nileshbucket58.
   Region: us-east-2.
2.Use Boto3 to interact with S3 and PyMySQL for database operations.

#### Configure Route 53 for Domain Mapping
1.Register a free domain (e.g., via Freenom).
2.In Route 53:
  Create a hosted zone for your domain.
  Add an A record pointing to your EC2 public IP address.
3.Test your domain to ensure it resolves to the application.

#### Application Features
1.Add Employee Records: Stores employee data (ID, name, skills, location) in RDS.
2.Upload Employee Images: Saves images to S3 and associates the URL with the record.
3.Dynamic Web Interface: Built with Flask templates.
4.Scalability: Hosted on AWS infrastructure for reliable performance.

#### Python Modules Used
Flask: Web framework.
PyMySQL: MySQL database connectivity.
Boto3: AWS SDK for Python.
MySQL-Client: For manual database operations.

#### Final Outcome
Employee data stored in RDS.
Images uploaded to S3.
Application accessible via your custom domain through Route 53.


You can copy this directly into a file named `README.md`. Let me know if you need any additional adjustments!


