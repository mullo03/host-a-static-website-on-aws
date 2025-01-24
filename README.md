Host a Static Website on AWS 

This repository contains resources, scripts, and a reference diagram to deploy a static HTML web application on AWS. The project demonstrates how to design and implement a secure, scalable, and fault-tolerant architecture using AWS services. 

1. Architecture Overview 

The project leverages the following AWS resources and design principles: 

Virtual Private Cloud (VPC) 

a. Configured with both public and private subnets across two availability zones for fault tolerance and high availability. 

b. Ensures logical network isolation for resources. 

Internet Gateway (IGW) 

a. Facilitates connectivity between VPC instances and the wider Internet. 

Security Groups 

a. Act as network firewalls to control inbound and outbound traffic to instances. 

Subnets 

a. Public Subnets: Used for infrastructure components like the NAT Gateway and Application Load Balancer. 

b. Private Subnets: Host web servers (EC2 instances) for enhanced security. 

NAT Gateway 

a. Allows instances in private subnets to securely access the Internet. 

EC2 Instances 

a. Host the static HTML website using Apache HTTP Server. 

b. Positioned in private subnets for improved security. 

Application Load Balancer (ALB) 

a. Distributes incoming traffic evenly across EC2 instances in the Auto Scaling Group. 

Auto Scaling Group (ASG) 

a. Automatically manages the number of EC2 instances to ensure availability and scalability. 

AWS Certificate Manager (ACM) 

a. Secures application communication using SSL/TLS certificates. 

Amazon Simple Notification Service (SNS) 

a. Sends notifications for events, such as Auto Scaling activities. 

Route 53 

a. Manages domain registration and DNS records for the hosted website. 

GitHub Repository 

a. Stores web application files for version control and collaboration. 

 

2. Deployment Instructions 

A. Prerequisites 

AWS Account with sufficient permissions to create and manage resources. 

A registered domain name. 

Git installed locally. 

B. Steps 

Clone this repository to your local machine: 

git clone https://github.com/mullo03/host-a-static-website-on-	aws.git 
 

Configure the AWS environment (VPC, subnets, security groups, IGW, and NAT Gateway). Use the reference diagram in this repository for guidance. 

Deploy an Auto Scaling Group with EC2 instances using the provided launch template script (see below). 

Configure the Application Load Balancer and target groups to distribute traffic to the EC2 instances. 

Secure communications with ACM by attaching an SSL/TLS certificate. 

Set up Route 53 to route traffic from the domain name to the Application Load Balancer. 

Enable notifications for the Auto Scaling Group using SNS. 

 

 

 

 

3. Launch Template Script 

Use the following script in the launch template to configure EC2 instances automatically: 

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
git clone https://github.com/mullo03/host-a-static-website-on-aws.git 
 
# Copy all files, including hidden ones, from the cloned repository to the Apache web root 
cp -R host-a-static-website-on-aws/. /var/www/html/ 
 
# Remove the cloned repository directory to clean up unnecessary files 
rm -rf host-a-static-website-on-aws 
 
# Enable the Apache HTTP Server to start automatically at system boot 
systemctl enable httpd 
 
# Start the Apache HTTP Server to serve web content 
systemctl start httpd

4. Features 

Scalability: 

a. Utilizes an Auto Scaling Group to maintain application performance during high traffic. 

Security: 

a. EC2 instances are hosted in private subnets. 

b. Traffic is secured with ACM SSL/TLS certificates. 

High Availability: 

a. Leverages multiple Availability Zones. 

b. Ensures fault tolerance through ALB and ASG configurations. 

5. Resources 

Reference architecture diagram (available in this repository). 

AWS documentation for VPC, ALB, ASG, ACM, SNS, and Route 53. 

6. Contact 

For questions or feedback, feel free to open an issue in this repository. 

Let me know if you’d like to customize any sections further! 

