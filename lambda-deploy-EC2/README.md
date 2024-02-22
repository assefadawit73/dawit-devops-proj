TABLE OF CONTENTS
Goal
Pre-Requisites
Automation
Validation
Lambda_AMI
Goal
Goals of this project to create weekly EC2 AMI backup of all EC2 instances running in the us-east-1 region and delete AMIs older than 30 days.

Pre-Requisites
Deploy Lambda Function as per the architecture shown above with required IAM roles.
Schedule Lambda Function to run weekly once Sunday 5 AM EST using cloudwatch event as Lambda trigger.
Create 5 EC2 instances with Tags  as “Name: dpt-web-server”
Create SNS topic and subscribe e-mail to receive notifications.
Automation
Write Python code as per the below high level requirement create AMI and delete old AMIs.
Describe list of all EC2 instances in us-east-1 region.
Get the list of EC2 Instance Ids as list data type
Get the EC2 Tag having key “Name”
Loop the list of Instance Ids and create AMI
Add tags to the AMI – Assign the EC2 Name tag to the AMI to identify which AMI belongs to which EC2 instance.
Add description to the AMI to understand the AMI belong to which server.
Add name to the AMI – Name includes server name (Get from Instance Tag) append with the date when the AMI created like “dpt-web-server-2021-12-23”
Delete the old unused AMIs which ever older than 30 days from the date of AMI creation.
Ensure that only unused AMIs are deleted, Skip the AMIs that are in use.
Print the AMIs that are deleted.
Print exceptions if any issues in creating or deleting AMI
Notify to SNS topic if any exceptions in creating or deleting AMI.
Deploy Python code to Lambda Function.
Validation
Run Lambda Function and verify AMI copy created for all EC2 instances with tags and deleted unused AMIs older than 30 days.