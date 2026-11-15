# AWS Infrastructure Architecture

## 1. Overview

The project uses a custom Amazon VPC to organize application and database infrastructure into separate public and private network segments.

The architecture demonstrates network isolation, HTTP traffic distribution, compute deployment, and secure database placement.

## 2. Network Configuration

| Component | Configuration |
|---|---|
| VPC | devops-3tier-vpc |
| VPC CIDR | 10.0.0.0/16 |
| Region | us-east-1 |
| Public Subnets | 2 |
| Private Subnets | 3 |
| Internet Gateway | 1 |

### Subnet Allocation

| Subnet | CIDR | Availability Zone |
|---|---|---|
| Public Subnet 1 | 10.0.1.0/24 | us-east-1a |
| Public Subnet 2 | 10.0.2.0/24 | us-east-1b |
| Private Subnet 1 | 10.0.3.0/24 | us-east-1a |
| Private Subnet 2 | 10.0.4.0/24 | us-east-1a |
| Private Subnet 3 | 10.0.5.0/24 | us-east-1b |

## 3. Application Layer

An Amazon EC2 instance running Amazon Linux 2023 hosted an Nginx web application.

The instance was deployed in a public subnet and served a static web page over HTTP.

An Application Load Balancer was configured across the two public subnets and forwarded HTTP traffic to the EC2 target.

The target group used the `/health` endpoint for health checks.

## 4. Database Layer

Amazon RDS for MySQL was deployed using a DB subnet group containing private subnets in two Availability Zones.

Database configuration:

- Engine: MySQL 8.4
- Instance class: db.t3.micro
- Storage: 20 GB gp3
- Encryption at rest: Enabled
- Public accessibility: Disabled
- Database port: 3306

Database access was restricted through a security group rule allowing traffic from the EC2 security group.

## 5. Traffic Flow

The intended HTTP traffic flow was:

1. Client sends an HTTP request to the Application Load Balancer.
2. The load balancer forwards the request to the registered EC2 target.
3. Nginx serves the application page.
4. The RDS database remains privately accessible and is not exposed to the internet.

Note: Application-to-database connectivity was not implemented or tested in this project.

## 6. Routing Design

- Public subnets used a route table with a default route to the Internet Gateway.
- Private subnets used a route table with local VPC routing only.
- No NAT Gateway was deployed to avoid additional hourly charges.

## 7. Architecture Limitations

The project is a foundational AWS infrastructure implementation rather than a fully production-ready three-tier application.

The following improvements are planned:

- Move application instances into private subnets.
- Configure HTTPS using AWS Certificate Manager.
- Implement application-to-database connectivity.
- Introduce Terraform for infrastructure automation.
- Add monitoring and centralized logging.

## 8. Resource Lifecycle

All project infrastructure was deleted after deployment validation to prevent ongoing resource charges.
