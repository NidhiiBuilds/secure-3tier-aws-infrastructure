# AWS Infrastructure Deployment Guide

## 1. Prerequisites

- AWS account with appropriate permissions.
- AWS Management Console access.
- AWS CloudShell with AWS CLI configured.
- Basic understanding of VPC, EC2, security groups and RDS.

## 2. Deployment Region

All project resources were deployed in:

`us-east-1` — US East (N. Virginia)

## 3. VPC and Networking Setup

1. Created a custom VPC named `devops-3tier-vpc`.
2. Configured the VPC CIDR as `10.0.0.0/16`.
3. Created two public subnets across two Availability Zones.
4. Created three private subnets.
5. Created and attached an Internet Gateway.
6. Configured a public route table with a default route to the Internet Gateway.
7. Associated the public subnets with the public route table.
8. Configured private subnet routing without a NAT Gateway.

## 4. Security Group Configuration

Created separate security groups for the application EC2 instance, Application Load Balancer and RDS database.

| Security Group | Inbound Configuration |
|---|---|
| ALB SG | HTTP port 80 and HTTPS port 443 rules |
| EC2 SG | HTTP port 80 from ALB SG; SSH port 22 from a restricted IP |
| RDS SG | MySQL port 3306 from EC2 SG |

Note: An HTTPS listener and certificate were not configured. The ALB served HTTP traffic.

## 5. EC2 Deployment

1. Launched an Amazon Linux 2023 EC2 instance.
2. Selected instance type `t3.micro`.
3. Deployed the instance in a public subnet.
4. Installed and configured Nginx using EC2 user data.
5. Created a static HTML application page.
6. Created a `/health` endpoint for load balancer health checks.
7. Verified application availability over HTTP.

## 6. Application Load Balancer Setup

1. Created an internet-facing Application Load Balancer.
2. Associated it with both public subnets.
3. Configured an HTTP listener on port 80.
4. Created a target group named `secure-3tier-tg`.
5. Registered the EC2 instance on port 80.
6. Configured the health check path as `/health`.
7. Verified that the registered target became healthy.
8. Tested application access through the ALB DNS endpoint.

## 7. RDS Database Deployment

1. Created a DB subnet group using private subnets in two Availability Zones.
2. Created an Amazon RDS MySQL database.
3. Selected MySQL 8.4 and instance class `db.t3.micro`.
4. Configured 20 GB gp3 encrypted storage.
5. Disabled public accessibility.
6. Configured the RDS security group to allow MySQL traffic only from the EC2 security group.
7. Validated database status, encryption and accessibility settings.

## 8. Validation

The infrastructure was validated using AWS CLI and HTTP requests.

Validation included:

- VPC and subnet configuration.
- Security group rules.
- EC2 application response.
- ALB target health.
- RDS database status.
- RDS encryption and public accessibility.

## 9. Cleanup

After validation, the project resources were deleted to avoid ongoing charges.

The cleanup included EC2, ALB, target group, RDS, subnets, security groups, route tables, Internet Gateway and the custom VPC.

## 10. Deployment Status

**Deployment and validation completed.**

The temporary AWS infrastructure was subsequently removed. This guide documents the deployment process and is not an active deployment script.
