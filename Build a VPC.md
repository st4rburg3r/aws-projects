<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Virtual Private Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-vpc)

**Author:** Trupti Vibhute  
**Email:** trupti.v19625@gmail.com

---

## Build a Virtual Private Cloud (VPC)

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-vpc_2facf927)

---

## Introducing Today's Project!

In this project, I will demonstrate how to create a VPC ... I'm doing this project to learn about networking in the cloud

### What is Amazon VPC?

Amazon VPC is our own private network inside the cloud... and it is useful because it isolates our environment from the entire cloud infrastructure

In today's project, I used Amazon VPC to creat a public subnet and connected a internet gateway to it

### Personal reflection

This project took me around 1 hr to complete

One thing I didn't expect in this project was for it to be this simple. I really enjoyed doing this project

---

## Virtual Private Clouds (VPCs)

### What I did in this step

In this step, I will Access the VPC console in AWS.

Create a VPC.

### How VPCs work

What's the point of having VPCs, why do they matter?
To put it simply - without VPCs, every AWS resource would exist in one giant, open space in the cloud, like a country without cities or districts.

Resources would be randomly scattered with no privacy or personal space, so everyone could see and access everyone else's resources 🙈

VPCs are the reason why resources can be made private to you. You also get control over resources in a VPC, so you can organize how they communicate and integrate with each other without the public internet.

p.s. if we're still a little unsure about the difference a VPC makes, here's another analogy that might help. Imagine if every file in Google Drive from any account was put into the same folder with no privacy or subfolders. You'd have to find your files amongst everything uploaded by everyone, which makes managing/securing your files really hard! That's what managing your resources would feel like without VPCs.

### Why there is a default VPC in AWS accounts

There was already a default VPC in my account ever since my AWS account was created. When you created your AWS account, AWS automatically sets up a default VPC for you! This default VPC is why you could launch resources (e.g. EC2 instances) and connect services together from Day 1 of using AWS. If it didn't exist, you would've had to learn how to create a VPC before you can use some of the services that need VPCs to function.

This default VPC is a handy starting point, especially for beginners, but you can always create custom VPCs to fit specific requirements e.g. strict security measures.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-vpc_2facf927)

### Defining IPv4 CIDR blocks

To set up my VPC, I had to define an IPv4 CIDR block, which is basially just a group of IP addresses written in a short format.

---

## Subnets

### What I did in this step

In this step, I will launch a subnet inside your VPC.

### Creating and configuring subnets

f your VPC is a city, subnets are like different neighborhoods inside your city. You use subnets to group resources with similar access rules and restrictions. Some subnets might be public areas that all resources can access (public subnets) while others are private areas with limited access (private subnets).

A VPC can have as many public and private subnets as you need, but subnets in the same VPC cannot have overlapping IP address CIDR blocks! This means each subnet must have a unique range of IP addresses.

The default VPC in your account comes with predefined subnets in each Availability Zone of a Region, which means you'll see 3 subnets on your page if your Region has 3 Availability Zones.

### Public vs private subnets

The difference between public and private subnet is that a public subnet is accessible through the internet and private subnet is not. ... For a subnet to be considered public, it has to be isolated from the internet access

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-vpc_157c4219)

### Auto-assigning public IPv4 addresses

Once I created my subnet, I enabled auto assign public ipv4 addresses
When you enable auto-assign public IPv4 address for a subnet, any EC2 instance launched in that subnet will instantly get a public IP address so you won't have to create one manually - a huge time saver!

---

## Internet gateways

### What I did in this step

Time for the last step in this project - let's attach your VPC with an internet gateway. This is like building a bridge (internet gateway) that links your private city (VPC) to the outside world (the internet), so your resources can communicate beyond your private space.



### Setting up internet gateways

An internet gateway connects your city (VPC) and the outside world (internet).

Internet gateways are key to making applications available on the internet. By attaching an internet gateway, your instances can access the internet and be accessible to external users.

Attaching an internet gateway means resources in your VPC can now access the internet. The EC2 instances with public IP addresses also become accessible to users, so your applications hosted on those servers become public too.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-vpc_4ae90410)

---

## Using the AWS CLI

### What I'm doing in this extension

In this project extension, I will Launch a VPC in Seconds with AWS CloudShell

### Exploring CloudShell and CLI

VPC resources could also be created with CloudShell, which is shell in your AWS Management Console, which means it's a space for you to run code. The awesome thing about AWS CloudShell is that it already has AWS CLI pre-installed. 

CLI is  software that lets you create, delete and update AWS resources with commands instead of clicking through your console.

### Debugging my setup

To set up a VPC or a subnet, you can use the command
aws ec2 create-subnet --vpc-id VPC-ID --cidr-block ADD-CIDR-BLOCK-HERE

Make sure to avoid errors by including the correct cidr block and make sure that the ip range is within the range of your vpc

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-vpc_9b2465411)

### Comparing CloudShell vs AWS Console

Compared to using the AWS Console, an advantage of using commands is it was a faster, more efficient way to do this project... Advantage of the aws conole is that t is beginner friendly and visual. Overall, I preferred setting everything up using the gui

---

---
