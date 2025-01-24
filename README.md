Host a Static Website on AWS

Project Overview

This project demonstrates how to host a static HTML web application on AWS using various AWS services to achieve high availability, scalability, and enhanced security. The project utilizes an EC2 instance to serve the website and implements multiple AWS resources to ensure optimal performance and fault tolerance. The full deployment setup, including reference architecture and scripts, is available on GitHub.

Features

1. Highly Available Infrastructure:

  Configured a Virtual Private Cloud (VPC) with public and private subnets across two availability zones for fault tolerance.

  Deployed an Internet Gateway to enable public connectivity for VPC instances.

2. Enhanced Security:

  Established Security Groups to act as network firewalls.

  Hosted web servers (EC2 instances) in private subnets to prevent direct access from the Internet.

  Utilized AWS Certificate Manager (ACM) to secure application communications.

3. Scalability and Resilience:

  Leveraged an Application Load Balancer (ALB) and target group to distribute traffic across EC2 instances.

  Configured an Auto Scaling Group to manage EC2 instances dynamically, ensuring elasticity and fault tolerance.

  Enabled instances in private subnets to access the Internet via a NAT Gateway.

4. Monitoring and Alerts:

  Configured Amazon Simple Notification Service (SNS) for notifications about activities within the Auto Scaling Group.

5. Domain Management:

  Registered a custom domain name and configured a DNS record using Route 53.

Architecture Overview

1. The architecture includes the following components:

VPC Configuration:

  Public and private subnets in two availability zones.

  Internet Gateway for public connectivity.

2. Network Security:

  Security Groups to allow only necessary traffic.

  EC2 Instance Connect Endpoint for secure connections to public and private subnets.

3. Web Hosting:

  EC2 instances running Apache HTTP Server to serve the static website.

  Web servers located in private subnets.

4. Load Balancing and Auto Scaling:

  Application Load Balancer for traffic distribution.

  Auto Scaling Group for instance management.

5. Domain and Certificates:

  Domain registered and managed via Route 53.

  SSL/TLS certificates provided by AWS Certificate Manager.

Deployment Steps

1. Clone the GitHub Repository

The website files and deployment scripts are hosted on GitHub. Clone the repository to access the necessary resources.

git clone https://github.com/mullo03/host-a-static-website-on-aws.git

2. Configure the EC2 Launch Template

The following script is used in the EC2 Launch Template to install required software, clone the website repository, and configure the Apache HTTP server:

#!/bin/bash
sudo su
yum update -y
yum install -y httpd
yum install git -y
cd /var/www/html
git clone https://github.com/mullo03/host-a-static-website-on-aws.git
cp -R host-a-static-website-on-aws/. /var/www/html/
rm -rf host-a-static-website-on-aws
systemctl enable httpd
systemctl start httpd

3. Deploy AWS Resources

VPC Configuration

Create a VPC with public and private subnets in two availability zones.

Attach an Internet Gateway to the VPC.

4. Security Groups

Define Security Groups to allow HTTP (port 80) and HTTPS (port 443) traffic to the ALB and restrict access to EC2 instances.

5. NAT Gateway

Deploy a NAT Gateway in a public subnet to allow private instances to access the Internet.

6. Application Load Balancer

Set up an ALB to handle incoming traffic and route it to the Auto Scaling Group's target instances.

7. Auto Scaling Group

Configure an Auto Scaling Group to dynamically add or remove EC2 instances based on traffic demand.

8. Route 53 Configuration

Register a domain name and set up a DNS record pointing to the ALB.

9. Monitoring and Alerts

Set up Amazon SNS to receive notifications for activities within the Auto Scaling Group, such as instance launches or terminations.

Benefits of the Architecture

1. High Availability: Utilization of multiple availability zones and an Auto Scaling Group ensures consistent website uptime.

2. Scalability: The system scales automatically based on traffic demand.

3. Security: Private subnets, NAT Gateway, and Security Groups ensure that the web servers are protected.

4. Ease of Management: Automation with scripts and AWS services reduces manual effort.

5. Cost-Effectiveness: The architecture optimizes resource utilization by scaling dynamically.

Resources

1. GitHub Repository

2. AWS Services Used: VPC, EC2, ALB, Auto Scaling Group, NAT Gateway, ACM, SNS, Route 53

Contribution

1. Contributions to improve this project are welcome! Please fork the repository and submit a pull request with your suggestions.
