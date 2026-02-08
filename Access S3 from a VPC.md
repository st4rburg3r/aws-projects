<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Access S3 from a VPC

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-s3)

**Author:** Trupti Vibhute  
**Email:** trupti.v19625@gmail.com

---

## Access S3 from a VPC

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-s3_3e1e79a2)

---

## Introducing Today's Project!

### What is Amazon VPC?

 AWS VPC (Virtual Private Cloud) is your own private, isolated section of the AWS cloud

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to access s3 buckets from my ec2 instance.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was for it to be thisss easyyyyyy.

### This project took me...

This project took me 40 mins.

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I will create a new VPC and launch an instance inside it.

### Step 2 - Connect to my EC2 instance

In this step, I will connect to my ec2 instance

### Step 3 - Set up access keys

In this step, I will give my ec2 instance the permission to access the aws s3 buckets.

---

## Architecture set up

I started my project by launching a vpc and creating a security group for resources in that vpc

I also uploaded 2 files in the bucket.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-s3_4334d777)

---

## Running CLI commands

There is a special software called the AWS CLI (Command Line Interface) that you install and run on your computer to control AWS services directly from the command line i.e. your terminal! You can install this in your local computer too, and all EC2 instances come with it already installed.



The first command I ran was aws s3 ls... This command is used to list all the s3 buckets in your AWS account.

The second command I ran was aws configure... This command is used to access those s3 buckets.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-s3_e7fa8776)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I had to configure the EC2 using my IAM access keys and secret key.

Access keys are are credentials for your applications and other servers to log into AWS and talk to your AWS services/resources.

The secret access key is like the password that pairs with your access key ID (your username). You need both to access AWS services.

### Best practice

Although I'm using access keys in this project, but the recommended way is to create an IAM role with the necessary permissions and then attaching that role to your EC2 instance.

---

## In the second part of my project...

### Step 4 - Set up an S3 bucket

In this step, I will Launch a bucket in Amazon S3.

### Step 5 - Connecting to my S3 bucket

In this step, I will :
Head back to your EC2 instance.

Get your EC2 instance to interact with your S3 bucket.



---

## Connecting to my S3 bucket

The first command I ran was aws s3 ls... This command is used to list all the s3 buckets in your AWS account.

When I ran the command aws s3 ls again, the terminal responded with the existing buckets in my aws account... This indicated that aws EC2 instance has the permission to access the buckets

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-s3_4334d778)

---

## Connecting to my S3 bucket

Another CLI command I ran was aws s3 ls s3://nextwork-vpc-project-trupti... which returned me the contents from that s3 bucket.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-s3_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command aws s3 cp /tmp/test.txt s3://nextwork-vpc-project-trupti... This command will copy the file i just created in the ec2 instance to the s3 buckets.

The second command I ran was aws s3 ls s3://nextwork-vpc-project-trupti.. 

DONEEEE

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-s3_3e1e79a2)

---

---
