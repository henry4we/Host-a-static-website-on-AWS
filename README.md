---

# Hosting a Static Website on AWS

This project demonstrates how to host a static HTML web application on AWS using various services and configurations. Below is an overview of the setup and deployment process.

## Project Overview

The project utilizes AWS services and configurations including:

1. **Virtual Private Cloud (VPC)**:
   - Configured with public and private subnets across multiple Availability Zones (AZs) for enhanced availability and security.

2. **Internet Gateway**:
   - Facilitates connectivity between VPC instances and the wider Internet.

3. **Security Groups**:
   - Acts as a network firewall to control traffic to EC2 instances.

4. **Availability Zones**:
   - Leveraged for deploying resources across multiple AZs to enhance reliability and fault tolerance.

5. **Public and Private Subnets**:
   - Public subnets host components like NAT Gateway and Application Load Balancer.
   - Private subnets are used for web servers (EC2 instances) to enhance security.

6. **EC2 Instance Connect Endpoint**:
   - Provides secure SSH connections to EC2 instances in public and private subnets.

7. **NAT Gateway**:
   - Allows instances in private subnets to access the Internet while remaining private.

8. **Web Hosting**:
   - Website files are stored on GitHub for version control and collaboration.

9. **Application Load Balancer (ALB)**:
   - Distributes incoming web traffic across an Auto Scaling Group of EC2 instances in multiple AZs.

10. **Auto Scaling Group**:
    - Automatically manages EC2 instances to ensure website availability, scalability, fault tolerance, and elasticity.

11. **Version Control and Collaboration**:
    - GitHub is used to store and manage web files.

12. **Certificate Manager**:
    - Secures application communications with SSL/TLS certificates.

13. **Simple Notification Service (SNS)**:
    - Configured to send notifications about activities within the Auto Scaling Group.

14. **Domain Name and DNS**:
    - Registered a domain name and set up DNS records using Route 53.

## Deployment Script

The deployment script (`deploy.sh`) automates the setup of the Apache HTTP Server and deployment of the static website:

```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su
# Update all installed packages to their latest versions
yum update -y
# Install Apache HTTP Server
yum install -y httpd
# Change the current working directory to the Apache web root
cd /var/www/html
# Install Git
yum install git -y
# Clone the project GitHub repository to the current directory
git clone https://github.com/henry4we/Host-a-static-website-on-AWS.git
# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R Host-a-static-website-on-AWS/. /var/www/html/
# Remove the cloned repository directory to clean up unnecessary files
rm -rf Host-a-static-website-on-AWS
# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd 
# Start the Apache HTTP Server to serve web content
systemctl start httpd
```


## Conclusion
This setup ensures a scalable, secure, and fault-tolerant environment for hosting a static web application, leveraging AWS's robust infrastructure.
---
