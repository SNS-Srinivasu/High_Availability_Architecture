# High_Availability_Architecture

![HA](https://github.com/user-attachments/assets/2a526255-d9c4-4b10-879a-35106b59db7e)



# Step-by-Step Setup

1. VPC and Subnet Configuration
Create a VPC with at least 2 public subnets in different Availability Zones.
Attach an Internet Gateway and configure route tables for internet access.
2. Launch Template
Create a Launch Template or Launch Configuration:
Use Amazon Linux 2 or preferred AMI.
Add a user data script to install Apache/NGINX web server.
Attach IAM Role for CloudWatch access.
Configure a Security Group allowing HTTP (80) and SSH (22).
3. Auto Scaling Group (ASG)
Create an ASG with the above Launch Template:
Spread across multiple AZs.
Set desired, minimum, and maximum instance counts.
Attach an Application Load Balancer for incoming traffic.
Configure scaling policies based on CPU utilization or traffic.
4. Application Load Balancer (ALB)
Create an ALB with:
Listener on port 80 (HTTP).
Target group with ASG-registered instances.
Health checks for endpoint monitoring (e.g., /index.html).
5. Route 53 Domain Setup
Register a domain or use an existing one.
Create a Hosted Zone.
Add an A Record (Alias) pointing to your ALB DNS.
6. Security Configuration
Configure Security Groups:
ALB SG: Allow HTTP (80) from 0.0.0.0/0.
EC2 SG: Allow HTTP from ALB SG, SSH from your IP.
Use NACLs for extra subnet-level filtering if required.
7. Monitoring & Alerts
Enable CloudWatch for:
Instance health and CPU usage.
ALB traffic metrics.
Auto Scaling events.
Set up CloudWatch Alarms and optionally connect to SNS for notifications.

# Outcome

Auto-scaled EC2 instances distributed across multiple AZs.
Traffic managed efficiently via ALB with health checks.
Secure and reliable access through Route 53 domain routing.
Real-time system visibility with CloudWatch.

# Key Learnings

How to build scalable and fault-tolerant infrastructure using AWS.
Automating instance management using Auto Scaling Groups.
Implementing DNS routing and health monitoring.
Designing with a security-first mindset using IAM, SGs, and CloudWatch.
