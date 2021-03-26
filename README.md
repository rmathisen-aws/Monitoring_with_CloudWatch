# Monitoring with CloudWatch

**Launch an EC2 Instance to Monitor:**\
EC2 → Launch Instance → Launch Instance \
Linux 2 AMI SSD (x86) \
t2.micro

Network: Default VPC \
Subnet: No Preference \
Auto-assign Public IP: Use subnet setting (Enable) \
**Monitoring:** Enable Cloudwatch Detailed Monitoring

By default, CloudWatch Data is available in 5 minute periods. \
Enabling Cloudwatch Detailed Monitoring **will cost more for data collection in 1 minute periods**, which may be useful for any production workloads.

Storage: Accept all defaults

Add Tag: Key: Name ... Value: cloudwatchEC2

Security Group: Accept all defaults

We'll be connecting into this Instance using a Web-based Terminal Application, so we don't need a Key Pair! \
Proceed without a Key Pair and acknowledge \

\
**Monitoring with CloudWatch:** \
Select the Instance → Monitoring Tab \
All of these Metrics are being delivered by CloudWatch!

In the top right of all of these metrics is a 3 dots dropdown menu. "View in Metrics" will redirect you to CloudWatch for more details on that Metric.

Next to the Refresh button is a dropdown. Enable Auto Refresh with a Refresh Interval. If you don't, you'll need to refresh manually.

CloudWatch → Metrics \
Notice all of the Namespaces available. All of the products that put info into CloudWatch have their own Namespace. \
ex: Billing, EBS, EC2, Logs, SNS, Usage \

\
**Create CloudWatch CPU Utilization Alarm:** \
CloudWatch → Alarms → Create Alarm \
Select Metric → EC2 → Per-Instance Metrics → check box for CPUUtilization → Select Metric \
Period: 1 minute \
Conditions: Static ... Greater ... 15 (represents CPU Utilization greater than 15%)

Once you set this, scroll back up and see the current Utilization in comparison to the threshold of 15%

Next

We can add a Notification for when the Alarm state is being triggered by creating a new SNS topic, or by using our existing Billing Alert topic, \
but click Remove to not allow any Notifications for this demo.

Next

Alarm Name: CPUUsageOver15Percent \
Next

Create Alarm

\
**Connect to EC2 Instance:** \
EC2 → Instances → Right Click the Instance → Connect → EC2 Instance Connect \
Make sure User name is ec2-user \
Connect

This connects us to the Instance using a Web-based Terminal connection!


\
**Stress our EC2 Instance to spike CPU Utilization:** \
Run: sudo amazon-linux-extras install epel -y \
This will give us additional repositories allowing us to install some applications

Run: sudo yum install stress -y \
This will install the Stress Utility

Run: stress \
If you see instructions on how to use this, that's confirmation that it installed correctly.

CloudWatch → Alarms → select CPUUsageOver15Percent alarm \
Notice the CPU Utilization Graph

Run: stress -c 2 \
This will Stress 2 CPU Cores of this instance

Refresh the Graph multiple times until you see the alarm move to "In Alarm" state 

Run: Ctrl+C \
This will cancel the Stress Test

Refresh the Graph multiple times until you see the alarm move to "OK" state

\
**Clean Up!!**
CloudWatch → Alarms → select CPUUsageOver15Percent → Actions → Delete → Delete

EC2 → Instances → Right Click cloudwatchEC2 Instance → Terminate Instance → Terminate

