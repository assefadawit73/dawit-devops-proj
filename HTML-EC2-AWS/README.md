## Goal
The goal of this project is to create weekly EC2 AMI backups of all EC2 instances running in the `us-east-1` region and delete AMIs older than 30 days.

## Pre-Requisites
1. Deploy Lambda Function with required IAM roles as per the architecture shown below.
2. Schedule Lambda Function to run weekly on Sundays at 5 AM EST using a CloudWatch event as the Lambda trigger.
3. Create 5 EC2 instances with tags as “Name: dpt-web-server”.
4. Create an SNS topic and subscribe an email to receive notifications.

## Automation
### High-Level Requirements
1. Write Python code to:
   - Describe and list all EC2 instances in the `us-east-1` region.
   - Get the list of EC2 instance IDs as a list data type.
   - Get the EC2 tag with the key “Name”.
   - Loop through the list of instance IDs and create AMIs.
   - Add tags to the AMI:
     - Assign the EC2 Name tag to the AMI to identify which AMI belongs to which EC2 instance.
     - Add a description to the AMI to understand which server the AMI belongs to.
     - Add a name to the AMI:
       - Name includes the server name (obtained from the instance tag) appended with the date when the AMI was created, like “dpt-web-server-2021-12-23”.
   - Delete old unused AMIs older than 30 days from the date of AMI creation.
     - Ensure that only unused AMIs are deleted; skip the AMIs that are in use.
     - Print the AMIs that are deleted.
     - Print exceptions if there are any issues in creating or deleting AMIs.
     - Notify the SNS topic if there are any exceptions in creating or deleting AMIs.
2. Deploy Python code to Lambda Function.

## Validation
1. Run Lambda Function and verify:
   - AMI copies are created for all EC2 instances with tags.
   - Unused AMIs older than 30 days are deleted.
