# Secure 3-Tier AWS Infrastructure

## Project Overview

This project demonstrates the design, deployment, security configuration, and validation of AWS infrastructure using core cloud networking and compute services.

The objective was to build a secure and scalable infrastructure foundation using a custom VPC, EC2, Application Load Balancer, and a private MySQL RDS database.

The infrastructure was deployed and validated using the AWS Management Console and AWS CLI.

## Objectives

- Design a custom AWS VPC with public and private subnets.
- Configure routing and internet connectivity.
- Deploy an Nginx web application on an EC2 instance.
- Configure an Application Load Balancer.
- Deploy an encrypted MySQL RDS database in private subnets.
- Implement security groups following least-privilege principles.
- Validate infrastructure configuration and clean up resources after testing.

## Architecture

The project uses the following infrastructure components:

- **Amazon VPC:** Custom network with CIDR `10.0.0.0/16`.
- **Public Subnets:** Two subnets across Availability Zones for internet-facing infrastructure.
- **Private Subnets:** Three subnets for private network placement and database subnet configuration.
- **Internet Gateway:** Provides internet connectivity to the public subnets.
- **Amazon EC2:** Hosts an Nginx web application.
- **Application Load Balancer:** Distributes HTTP traffic to the EC2 target.
- **Amazon RDS:** MySQL database configured in private subnets with encryption enabled.
- **Security Groups:** Control traffic between infrastructure components.

## Project Documentation

Detailed documentation is available below:

- [Architecture](docs/architecture.md)
- [Deployment Guide](docs/deployment-guide.md)
- [Security Design](docs/security-design.md)
- [Testing and Validation](docs/testing-and-validation.md)

## AWS Services Used

| Service | Purpose |
|---|---|
| Amazon VPC | Network isolation |
| EC2 | Application hosting |
| Application Load Balancer | HTTP traffic distribution |
| Amazon RDS | Managed MySQL database |
| IAM / AWS account permissions | Resource access management |
| AWS CLI | Deployment and validation |

## Implementation

1. Created a custom VPC with public and private subnets across multiple Availability Zones.
2. Configured route tables and an Internet Gateway.
3. Created security groups to control application, load balancer, and database traffic.
4. Launched an EC2 instance and deployed an Nginx web page.
5. Configured an Application Load Balancer and registered the EC2 instance as a target.
6. Verified target health and HTTP application availability.
7. Created an encrypted MySQL RDS database in private subnets.
8. Validated database accessibility settings, encryption, and security group configuration.
9. Deleted project resources after completing validation to avoid ongoing infrastructure charges.

## Security Considerations

- RDS was configured with encryption at rest.
- RDS public accessibility was disabled.
- Database traffic was restricted to the EC2 security group.
- The EC2 instance was deployed in a public subnet, while RDS remained in private subnets.
- Security groups were configured to control inbound traffic.

**Note:** The application-to-database connection was not implemented or tested.

## Testing and Validation

The following checks were performed:

- Verified VPC, subnet, and route table configuration.
- Confirmed Nginx application availability through HTTP.
- Verified the Application Load Balancer target health.
- Confirmed RDS engine, encryption, and private accessibility settings.
- Used AWS CLI to validate resource configuration.
- Verified cleanup of deployed infrastructure.

## Cost Management and Cleanup

To minimize costs:

- No NAT Gateway was deployed.
- Temporary infrastructure was used for validation.
- EC2, ALB, RDS, and associated project networking resources were deleted after testing.
- No project-owned EBS snapshots or Elastic IPs remained during final validation.

## Project Outcome

Successfully designed, deployed, tested, and cleaned up a foundational AWS infrastructure environment using core networking, compute, load balancing, database, and security services.

This project strengthened practical understanding of AWS infrastructure deployment, network isolation, traffic management, security group configuration, database security, and resource lifecycle management.

The application-to-database connection was not implemented, and HTTPS was not configured. The project focuses on infrastructure deployment and validation.

## Future Improvements

- Automate infrastructure provisioning using Terraform.
- Implement HTTPS using AWS Certificate Manager.
- Deploy the application in private subnets.
- Integrate the application with the RDS database.
- Introduce CI/CD automation.
- Add monitoring and centralized logging.

## Author

**Nidhii Builds**

GitHub: https://github.com/NidhiiBuilds
