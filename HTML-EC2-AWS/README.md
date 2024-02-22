TABLE OF CONTENTS
Goal
Pre-Requisites
Pre-Deployment
Deployment
Post-Deployment
Validation
AWS Static web site deployment

Goal
Deploy HTML based static website on Amazon EC2 instance and configure logging, monitoring, alerts.  This project hosting static web application on Apache Web Server to serve the web pages to internet clients. 

Pre-Requisites
You must be having an AWS account to create infrastructure resources on AWS cloud.
Source Code
Pre-Deployment
Customize the application dependencies mentioned below on AWS EC2 instance and create the Golden AMI.

AWS CLI
Install Apache Web Server
Install Git
Configure Apache to start automatically after the instance reboot.
Deployment
Infrastructure Setup

Create Security Group allowing port 22 from custom IP source ( Your workstation IP ) and port 80 from public.
Create Key-Pair and download the private key.
Create t2.micro type EC2 instance using Golden AMI. 
Create Elastic IP and associate the IP to EC2 instance.
Create GP2 type EBS volume named /dev/xvdb of size 5GB in same AZ where EC2 was created.
Attach EBS volume to EC2 instance.
Create Route53 hosted zone with your domain name and configure A record pointing to the EC2 EIP.
Create private S3 bucket and enable versioning.
Application Setup

Create File System on xvdb volume and mount it on /var/www/html directory. 
Use Git commands and clone the source code from Bit Bucket repository provided in the pre-requisites.  ()
Deploy the source code into web server document root folder – /var/www/html
Post-Deployment
Configure Cloudwatch agent to monitor Memory utilization of EC2 instance.
Create Cloudwatch Dashboard to monitor CPU & Memory metrics of the EC2 instance.
Configure SNS topic and subscribe e-mail to the Topic.
Configure Cloudwatch alarm with 1 data point and 5 minutes interval rate to notify to SNS topic when average CPU utilization is greater than 80% threshold.
Configure Cloudwatch alarm with 1 data point and 5 minutes interval rate to notify to SNS topic when average Memory utilization is greater than 60% threshold. 
Use AWS CLI commands to push webserver logs to S3 bucket.
Configure S3 life cycle rules to transit previous version objects to Glacier after 30 days and delete the objects after 90 days of object creation date.
Validation
Verify if you are able to access the web application from internet browser