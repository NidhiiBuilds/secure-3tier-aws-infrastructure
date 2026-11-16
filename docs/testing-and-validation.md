# Testing and Validation

## Objective
To verify that the AWS infrastructure was deployed successfully and its main components were working as expected.

## Testing Performed

- **VPC:** Verified VPC, subnet and routing configurations.
- **EC2:** Confirmed that the Nginx web application was accessible.
- **ALB:** Verified healthy target status and successful HTTP response (200).
- **RDS:** Confirmed database status was available, encryption was enabled and public access was disabled.
- **Security Groups:** Verified access restrictions between infrastructure components.

## Test Results

| Component | Result |
|---|---|
| VPC and Networking | Passed |
| EC2 Application | Passed |
| ALB Health Check | Passed |
| RDS Configuration | Passed |
| Application-to-RDS Connection | Not tested |
| HTTPS | Not configured |

## Conclusion

The core infrastructure was successfully deployed and validated. After testing, the AWS resources were deleted to avoid ongoing charges.
