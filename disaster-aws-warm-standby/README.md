# Deploy Disaster Recovery of Workloads on AWS: Warm Standby

![image](https://github.com/assefadawit73/dawit-devops-proj/assets/66095194/e884510e-c10c-4956-82ac-c0a7efd17548)


## TABLE OF CONTENTS

1. [Project](#project)
2. [Pre-Requisites](#pre-requisites)
3. [Deployment](#deployment)
4. [Verification](#verification)

## Project
The goal of this project is to deploy scalable, highly available, and secured web applications in AWS Multi-Region for a Disaster Recovery solution on the Cloud.

### AWS Disaster Recovery: Active Standby

## Pre-Requisites
- Create an S3 Bucket and PUT index.html file.
- Register a domain in Route 53.

## Deployment
Below are the high-level steps to implement the project:

### us-east-1:
1. Create Golden AMI with all pre-requisites to set up a webserver.
   - Install Apache Webserver
2. Copy Golden AMI to us-west-1 region.
3. Create VPC
   - CIDR: 172.32.0.0/16
4. Deploy Internet Facing Application Load balancer with below configuration
   - Listening Port 443
   - Associate SSL from ACM.
5. Deploy Launch Configuration and auto-scaling group for Webserver.
   - Min: 2
   - Max: 4
   - Associate Subnets from two AZs (us-east-1a & us-east-1b)
   - Customize Launch Configuration user-data to automate the software provisioning for the webserver.
   - Download the index.html (Artifact) from S3 and deploy to the root folder
   - Start Apache Webserver
   - Associate IAM Role with Session Manager and S3 Policies.
   - Associate Target Group to Auto Scaling Group.
   - Configure SNS notification on auto-scaling Group event change.
   - Configure scaling policy to scale out when CPU utilization breaches the threshold 80% utilization.
   - Configure scaling policy to scale in when CPU utilization below the threshold 80% utilization.

### us-west-1:
1. Create VPC
   - CIDR: 172.33.0.0/16
2. Create VPC Peering between the two VPCs in two Regions and update the route tables accordingly to have private communication between the VPCs.
3. Deploy Internet Facing Application Load balancer with below configuration
   - Listening Port 443
   - Associate SSL from ACM.
4. Deploy Launch Configuration and auto-scaling group for Webserver.
   - Min: 1
   - Max: 3
   - Associate Subnets from two AZs (us-west-1a & us-west-1b)
   - Customize Launch Configuration user-data to automate the software provisioning for the webserver.
   - Download the index.html (Artifact) from S3 and deploy to the root folder
   - Start Apache Webserver
   - Associate IAM Role with Session Manager and S3 Policies.
   - Associate Golden AMI
   - Associate Target Group to Auto Scaling Group.
   - Configure SNS notification on auto-scaling Group event change.
   - Configure scaling policy to scale out when CPU utilization breaches the threshold 80% utilization.
   - Configure scaling policy to scale in when CPU utilization below the threshold 80% utilization.

### Global:
- Create Resource Record in Route 53 with “Failover routing policy”
   - Primary Record pointing to ALB in us-east-1 region
   - Standby Record pointing to ALB in us-west-1 region

## Verification
You may manually fail the resource to test the below scenario.
- AZ Failures
- Instance Failures
- Region Failures
- Apache Webserver Service Failures

