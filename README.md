![Alt text](/Host_a_Static_Website_on_AWS (1).png)

# Hosting a Static Website on AWS

## Project Overview
This project involves hosting a static HTML web application on Amazon Web Services (AWS), utilizing various services to ensure scalability, reliability, and security. The project demonstrates the deployment of a web application using AWS infrastructure including EC2 instances, VPC configurations, load balancing, and auto-scaling capabilities.

## Architecture
The architecture utilizes a Virtual Private Cloud (VPC) with public and private subnets spread across two Availability Zones (AZs). Key components and configurations include:

- **VPC Configuration**: To enhance reliability, it is set up with public and private subnets across two different Availability Zones.
- **Internet Gateway**: Facilitates connectivity between VPC instances and the wider Internet.
- **Security Groups**: Acts as a network firewall to define rules for inbound and outbound traffic.
- **Application Load Balancer (ALB)**: Distributes incoming web traffic across multiple EC2 instances for improved performance and availability.
- **NAT Gateway**: Allows instances in private subnets to access the Internet while remaining unreachable from the public Internet.
- **Auto Scaling Group (ASG)**: Automatically manages EC2 instances, ensuring application availability and scalability based on traffic demands.
- **Certificate Manager**: Secures application communications using SSL certificates.

## Implementation Steps
1. **Setup Environment**: Configure the AWS environment including VPC, subnets, and load balancers.
2. **Launch EC2 Instances**: Deploy EC2 instances in private subnets to host the static website.
3. **Web Server Installation**: Install and configure Apache HTTP Server on the EC2 instances using the provided script.
4. **Deployment of Static Files**: Clone the GitHub repository containing the web files and move them to the Apache web root.

## Deployment Script
Below is the shell script used to set up the environment on the EC2 instances:

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
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/
# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws
# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd
# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

## Additional Setup
- **Route 53**: Registered the domain name and configured DNS records to point to the Application Load Balancer.
- **SNS**: Configured Simple Notification Service to send alerts regarding activities within the Auto Scaling Group.

## Version Control
All project files are stored on GitHub for version control and collaboration. The repository can be found at: [GitHub Repository](https://github.com/aosnotes77/host-a-static-website-on-aws)

## Conclusion
This project serves as a comprehensive example of deploying a static website on AWS using best practices for security, performance, and scalability. Using various AWS services ensures that the application can handle varying loads while remaining secure.

---


