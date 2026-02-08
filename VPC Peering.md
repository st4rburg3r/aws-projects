<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-peering)

**Author:** Trupti Vibhute  
**Email:** trupti.v19625@gmail.com

---

## VPC Peering

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is like a private space for you inside the entire cloud infrastructure.... and it is useful because it isolates our resources from others.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create 2 new VPCs and set up a peering connection between them.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was even tho it was mildly psicy, I completed it in really less time as my basics were really strong.

### This project took me...

This project took me 1 hr.

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, get ready to:
Create two VPCs from scratch!
Use the visual VPC resource map to create your VPCs supa fast

### Step 2 - Create a Peering Connection

In this step, I will Set up a connection link between  VPCs.

### Step 3 - Update Route Tables

In this step, I wil;:

Set up a way for traffic coming from VPC 1 to get to VPC 2.

Set up a way for traffic coming from VPC 2 to get to VPC 1.

### Step 4 - Launch EC2 Instances

In this step, I will Launch an EC2 instance in each VPC, so we can use them to test your VPC peering connection later.

---

## Multi-VPC Architecture

I started my project by creating 2 new VPCs, each with 1 public subnet and 0 private subnets.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16... Each VPC must have a unique IPv4 CIDR block so the IP addresses of their resources don't overlap. Having overlapping IP addresses could cause routing conflicts and connectivity issues!

### I also launched 2 EC2 instances

I didn't set up key pairs for these EC2 instances as In previous projects, setting up a key pair was a key step for learning how SSH and directly accessing an EC2 instance works.

However, we've also learnt that with EC2 Instance Connect, AWS actually manages a key pair for us! We don't need to manage key pairs ourselves. Since we've already learnt how to set up key pairs twice in the last two projects, we don't need to do it again this time.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is a direct connection between two VPCs.

A peering connection lets VPCs and their resources route traffic between them using their private IP addresses. This means data can now be transferred between VPCs without going through the public internet.

Without a peering connection, data transfers between VPCs would use resources' public address - meaning VPCs have to communicate over the public internet. 

In VPC peering, the Requester is the VPC that initiates a peering connection. As the requester, they will be sending the other VPC an invitation to connect!

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

Even if your peering connection has been accepted, traffic in VPC 1 won't know how to get to resources in VPC 2 without a route in your route table! You need to set up a route that directs traffic bound for VPC 2 to the peering connection you've set up.

My VPCs' new routes have a destination of the other vpc CIDR block... The routes' target was the peering connection

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I will: 
Use EC2 Instance Connect to connect to your first EC2 instance.

Fix a connection error!



### Step 6 - Connect to EC2 Instance 1

In this step, I will: 
Use EC2 Instance Connect to connect to Instance 1 (one more time)!

Fix (another) error.

### Step 7 - Test VPC Peering

In this step, I will:
Get Instance 1 to send test messages to Instance 2.

Solve connection errors until Instance 2 is able to send messages back.

---

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to connect the instance without having to manage the key pairs.

I was stopped from using EC2 Instance Connect as my EC@ instance 1 had no public address.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, I set up Elastic IP addresses. Elastic IPs are static IPv4 addresses that get allocated to your AWS account, and is yours to delegate to an EC2 instance.

Associating an Elastic IP address resolved the error because now that instance has been assigned a public ipv4 address using elastic ip.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I ran the command ping <private ip of instance 2>

A successful ping test would validate my VPC peering connection because This means that the ICMP (Internet Control Message Protocol) traffic is now successfully reaching Instance - NextWork VPC 2, thanks to the adjustments you made in the network ACLs and Security Groups. Nice! 

I had to update my second EC2 instance's security group because there was no rule to allow icmp ping requests. Thats why i was getting no response for the ping command.... I added a new rule that allows ICMP requests from the VPC1.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-peering_7a29d352)

---

---
