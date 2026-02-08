<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Endpoints

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-endpoints)

**Author:** Trupti Vibhute  
**Email:** trupti.v19625@gmail.com

---

## VPC Endpoints

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-endpoints_09bcaa8a)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC lets you organize your cloud region into sections which act as your own data centre where you can launch resources.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to Access my S3 buckets through a VPC endpoint.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was going through the steps again and again for troubleshooting.

### This project took me...

This project took me 1.5 hours

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I will :
Create a VPC from scratch!

Launch an EC2 instance, which you'll connect to using EC2 Instance Connect later.

Set up an S3 bucket.

### Step 2 - Connect to EC2 instance

In this step, I am  gonna connect to the EC2 instance and try access S3 through the public internet!



### Step 3 - Set up access keys

In this step, I will Give the EC2 instance access to my AWS environment.

### Step 4 - Interact with S3 bucket

In this step, I will:
Head back to my EC2 instance.

Get your EC2 instance to access my S3 bucket.

---

## Architecture set up

I started my project by launching a new vpc, ec2 inscance.

I also set up the s3 bucket with 3 files inside it.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-endpoints_4334d777)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I created an access key and a secret access key, which i tel entered in the ec2 CLI to give my instance the permission to access to the buckets

An access key ID is a part of a credential!

Your credentials are made up of a username and password; think of the access key ID as the username.

You don't automatically have one, but you can create access keys IDs through AWS IAM.

The secret access key is like the password that pairs with your access key ID (your username). You need both to access AWS services.

Secret is a key word here - anyone who has it can access your AWS account, so we need to keep this away from anyone else!

### Best practice

Although I'm using access keys in this project, a best practice alternative is to make an IAM user and attach those rueles to your EC2 instance.

---

## Connecting to my S3 bucket

The command I ran was aws s3 ls... This command is used to ist the S3 buckets in your account (yup, ls stands for list!).

The terminal responded with all the buckets present in my AWS account... This indicated that the access keys I set up were woking!

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-endpoints_4334d778)

---

## Connecting to my S3 bucket

I also tested the command aws s3 ls s3://nextwork-vpc-project-maya... which returned me the contents of my bucket.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-endpoints_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command 'sudo touch /tmp/nextwork.txt'... This command creates a new text file.

The second command I ran was 'aws s3 cp /tmp/nextwork.txt s3://nextwork-vpc-project-trupti'... This command will copy the text file i had just made to my aws s3 buckets folder.

The third command I ran was 'aws s3 ls s3://nextwork-vpc-project-.trupti'.. which validated that my new file was aded tomy S3 bucket.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-endpoints_3e1e79a2)

---

## In the second part of my project...

### Step 5 - Set up a Gateway

In this step, I will:
Set up a way for my VPC and S3 to communicate direclty.

### Step 6 - Bucket policies

Limit your S3 bucket access's to only traffic from your endpoint.

### Step 7 - Update route tables

In this step, I will:
Test the VPC endpoint set up.

Troubleshoot a connectivity issue

### Step 8 - Validate endpoint conection

In this step, I will:
Test my VPC endpoint set up (again).

Restrict my VPC's acccess to your AWS environment

---

## Setting up a Gateway

I set up an S3 Gateway, which is...

### What are endpoints?

An endpoint is a way to communicae too the external AWS services from your vpc-- without routing the traffic over the internet.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-endpoints_09bcaa8a)

---

## Bucket policies

A bucket policy is a type of IAM policy designed for setting access permissions to an S3 bucket. Using bucket policies, you get to decide who can access the bucket and what actions they can perform with it.

This policy denies all actions (s3:*) on your S3 bucket and its objects to everyone (Principal: "*")... unless the access is from the VPC endpoint with the ID defined in aws:sourceVpce.

In other words, only traffic coming from your VPC endpoint can get any access to your S3 bucket!

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-endpoints_7316a13d)

---

## Bucket policies

Your policy denies all actions unless they come from your VPC endpoint. This means any attempt to access your bucket from other sources, including the AWS Management Console, is blocked!

I also had to update my route table because there was no route through the vpc to the the external aws services.

he route table is the GPS / traffic controller directing traffic from your EC2 instances.

If your route table doesn't have a route that directs traffic bound for S3 to your VPC endpoint, traffic from your EC2 instance is actually trying to get to your S3 bucket through the public internet instead.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-endpoints_4ec7821f)

---

## Route table updates

To update my route table, added a new route where the destination was the s3 bucket and target was the vpc endpoint i had created.

After updating my public subnet's route table, my terminal could return the contents from the s3 bucket


![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-endpoints_d116818e)

---

## Endpoint policies

An endpoint policy is a set of rules created by an organization to secure the devices (endpoints) that connect to its network

Updated the endpoint policy so that i wont be able to access the s3 buckets through mycloudshell terminal.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-endpoints_3e1e79a3)

---

---
