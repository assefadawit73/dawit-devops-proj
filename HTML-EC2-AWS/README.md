
# Deploy HTML based static web application on AWS EC2

![image](https://github.com/assefadawit73/dawit-devops-proj/assets/66095194/4c53cffa-4cd0-410e-86be-a302f48e00d5)


## TABLE OF CONTENTS

1. [Goal](#goal)
2. [Pre-Requisites](#pre-requisites)
3. [Pre-Deployment](#pre-deployment)
4. [Deployment](#deployment)
5. [Post-Deployment](#post-deployment)
6. [Validation](#validation)
7. [AWS Static web site deployment](#aws-static-web-site-deployment)

## Goal
Deploy an HTML-based static website on an Amazon EC2 instance and configure logging, monitoring, and alerts. This project hosts a static web application on an Apache Web Server to serve web pages to internet clients.

## Pre-Requisites
- You must have an AWS account to create infrastructure resources on the AWS cloud.
- Source Code

## Pre-Deployment
1. Customize the application dependencies mentioned below on AWS EC2 instance and create the Golden AMI.
   - AWS CLI
   - Install Apache Web Server
   - Install Git
   - Configure Apache to start automatically after the instance reboot.

## Deployment
### Infrastructure Setup
- Create Security Group allowing port 22 from custom IP source (Your workstation IP) and port 80 from public.
- Create Key-Pair and download the private key.
- Create t2.micro type EC2 instance using Golden AMI.
- Create Elastic IP and associate the IP to EC2 instance.
- Create GP2 type EBS volume named /dev/xvdb of size 5GB in the same AZ where EC2 was created.
- Attach EBS volume to EC2 instance.
- Create Route53 hosted zone with your domain name and configure A record pointing to the EC2 EIP.
- Create private S3 bucket and enable versioning.

### Application Setup
- Create File System on xvdb volume and mount it on /var/www/html directory.
- Use Git commands and clone the source code from BitBucket repository provided in the pre-requisites.
- Deploy the source code into web server document root folder – /var/www/html.

## Post-Deployment
- Configure Cloudwatch agent to monitor Memory utilization of EC2 instance.
- Create Cloudwatch Dashboard to monitor CPU & Memory metrics of the EC2 instance.
- Configure SNS topic and subscribe e-mail to the Topic.
- Configure Cloudwatch alarm with 1 data point and 5 minutes interval rate to notify to SNS topic when average CPU utilization is greater than 80% threshold.
- Configure Cloudwatch alarm with 1 data point and 5 minutes interval rate to notify to SNS topic when average Memory utilization is greater than 60% threshold.
- Use AWS CLI commands to push web server logs to S3 bucket.
- Configure S3 life cycle rules to transit previous version objects to Glacier after 30 days and delete the objects after 90 days of object creation date.

## Validation
- Verify if you are able to access the web application from an internet browser.
