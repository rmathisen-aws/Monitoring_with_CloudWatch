# Monitoring with CloudWatch

**Launch an EC2 Instance to Monitor:**\
EC2 → Launch Instance → Launch Instance \
Linux 2 AMI \
t2.micro

Network: Default VPC \
Subnet: No Preference \
Auto-assign Public IP: Use subnet setting (Enable) \
**Monitoring:** Enable Cloudwatch Detailed Monitoring

By default, CloudWatch Data is available in 5 minute periods. \
Enabling Cloudwatch Detailed Monitoring **will cost more for data collection in 1 minute periods**, which may be useful for any production workloads.

