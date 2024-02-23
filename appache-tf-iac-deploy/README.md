# Deploy Apache Web Server using Terraform IaC

![image](https://github.com/assefadawit73/dawit-devops-proj/assets/66095194/67cdbbe8-6da0-48ec-b795-8071be836c3c)


## TABLE OF CONTENTS

1. [Goal](#goal)
2. [Pre-Requisites](#pre-requisites)
3. [Deployment](#deployment)
4. [Validation](#validation)
5. [Destroy](#destroy)
6. [Terraform_IaC_Webserver](#terraform_iac_webserver)

## Goal
The goal of this project is to write Terraform Infrastructure as Code (IaC) to deploy an Apache Webserver in the AWS cloud.

## Pre-Requisites
- Create the following resources using Terraform IaC:
  - S3 Bucket to store the Terraform state files
  - DynamoDB
  - Deploy VPC Network using Terraform IaC and keep the state file in S3 backend.
- Create the following resources using Terraform IaC and keep the state file in S3 backend:
  - S3 Bucket to store the webserver configuration and PUT `user-data.sh` script file which will configure the webserver
  - SNS topic for notifications
  - IAM Role
  - Golden AMI

## Deployment
1. Write Terraform IaC to deploy the following resources in the VPC that was created in the Pre-Requisites step and keep the state file in S3 backend with state locking support:
   - Create IAM Role granting PUT/GET access to S3 Bucket and Session Manager access.
   - Create Launch Configuration with userdata script to pull the `user-data.sh` file from S3 and attach IAM role (user-data.sh will configure the webserver).
   - Create Auto Scaling Group with Min:1 Max:1 Desired:1 in private subnet.
   - Create Target Group with health checks and attach with Auto Scaling Group.
   - Create Application Load Balancer in public subnet and configure Listener Port to route the traffic to the Target Group.
   - Create alias record in Hosted Zone to route the traffic to the Load balancer from the public network.
   - Create CloudWatch Alarms to send notifications when ASG state changes.
   - Create Scaling Policies to scale out/Scale In when average CPU utilization is > 80%.
2. Deploy Terraform IaC to create the resources.

## Validation
- Login to AWS Console and verify all the resources are deployed.
- Access the web application from a public internet browser using the domain name.

## Destroy
Destroy the resources once the testing is over to save the billing.
