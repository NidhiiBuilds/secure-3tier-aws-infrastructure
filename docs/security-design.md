# Security Design – AWS 3-Tier Infrastructure

## 1. Objective

The objective of the security design was to restrict unnecessary network access, separate application and database access, and protect stored database data.

## 2. Network Security

- Created a custom VPC with CIDR `10.0.0.0/16`.
- Separated public and private subnets.
- Placed the Application Load Balancer and EC2 application server in public subnets.
- Placed the RDS database in private subnets.
- Did not configure a NAT Gateway, avoiding additional infrastructure cost.

## 3. Security Group Configuration

Separate security groups were configured for the ALB, EC2 instance, and RDS database.

| Component | Access Configuration |
|---|---|
| ALB | HTTP traffic allowed on port 80 |
| EC2 | HTTP traffic allowed from the ALB security group |
| EC2 SSH | SSH access restricted to a specific public IP during deployment |
| RDS | MySQL port 3306 allowed only from the EC2 security group |

This configuration restricted direct database access from the public internet.

## 4. Database Security

The Amazon RDS MySQL database was configured with:

- Private accessibility enabled (public access disabled).
- Encryption at rest enabled.
- A dedicated database security group.
- MySQL access restricted to the EC2 security group.
- A DB subnet group spanning private subnets in two Availability Zones.

## 5. Application Access

- The application was hosted using Nginx on an EC2 instance.
- The Application Load Balancer provided the application entry point.
- Target health was monitored using the `/health` endpoint.
- Application access was tested over HTTP.

## 6. Security Limitations

The project demonstrates foundational cloud security practices but is not fully production-ready.

Known limitations:

- HTTPS and SSL/TLS certificates were not configured.
- The EC2 application server was deployed in a public subnet.
- The application-to-database connection was not implemented or tested.
- IAM role-based application access was not implemented as part of this project.
- Advanced monitoring and centralized logging were not configured.

## 7. Future Security Improvements

- Move application servers into private subnets.
- Configure HTTPS using AWS Certificate Manager.
- Implement IAM roles and least-privilege permissions.
- Enable enhanced monitoring and centralized logging.
- Configure stronger backup and disaster recovery policies.
- Integrate the application securely with the RDS database.

## 8. Conclusion

The project implemented network segmentation, security-group-based access restrictions, private database deployment, and database encryption. These measures demonstrate an understanding of essential AWS infrastructure security concepts.
