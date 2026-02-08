<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Monitoring with Flow Logs

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-monitoring)

**Author:** Trupti Vibhute  
**Email:** trupti.v19625@gmail.com

---

## VPC Monitoring with Flow Logs

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-monitoring_3e1e79a1)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is like a privatre space for your cloud resources... and it is useful because it seperates your network from the entire cloud infrastructure.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to learn more about vpc peering, cloudwatch and log monitoring

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was-- i left my pc on during the pings, and ping was running for almost two hours. 
I hope my free credits are still $120.

### This project took me...

This project took me 1 hr (if u dont count the 2 hr where i was afk)

---

## In the first part of my project...

### Step 1 - Set up VPCs

In this step, I will Create two VPCs from scratch!

### Step 2 - Launch EC2 instances

In this step, I will launce EC2 instances in each of the vpc

### Step 3 - Set up Logs

In this step, I will :
Set up a way to track all inbound and outbound network traffic.

Set up a space that stores all of these records.



### Step 4 - Set IAM permissions for Logs

In this step, I will:
Give VPC Flow Logs the permission to write logs and send them to CloudWatch.

Finish setting up subnet's flow log.

---

## Multi-VPC Architecture

I started my project by launching 2 vpcs using the vpc wizard.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16... Each VPC must have a unique IPv4 CIDR block so the IP addresses of their resources don't overlap. Having overlapping IP addresses could cause routing conflicts and connectivity issues!...

### I also launched EC2 instances in each subnet

My EC2 instances' security groups allow Allow ICMP traffic from ALL IP addresses...

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-monitoring_e7fa8775)

---

## Logs

Logs are like a diary for your computer systems. They record everything that happens, from users logging in to errors popping up. It's the go-to place to understand what's going on with your systems, troubleshoot problems, and keep an eye on who’s doing what.

Think of a log group as a big folder in AWS where you keep related logs together. Usually, logs from the same source or application will go into the same log group, BUT logs are also region-specific. This means log data gets created and saved in the region it was created, although you can use CloudWatch dashboards to bring together logs from different regions.

### I also set up a flow log for VPC 1

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-monitoring_e8398869)

---

## IAM Policy and Roles

I created an IAM policy because VPC Flow Logs doesn't have the permission to write logs and send them to CloudWatch..

IAM policies and roles go hand in hand, so it's important to know their differences and how they work together!

IAM policies are like rules that determine what someone/something can or cannot do in your AWS account.

When you bundle IAM policies together, you create an IAM role. You then assign this role to AWS services or users, giving them the permissions included in the attached policies.

A custom trust policy is specific type of policy! They're different from IAM policies. While IAM policies help you define the actions a user/service can or cannot do, custom trust policies are used to very narrowly define who can use a role.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-monitoring_4334d777)

---

## In the second part of my project...

### Step 5 - Ping testing and troubleshooting

Let's generate some network traffic and see whether our flow logs can pick up on them.

We're going to generate network traffic by trying to get our instance in VPC 1 to send a message to our instance in VPC 2.

Since we're trying to get our instances to talk to each other, this means we're also testing our VPC peering setup at the same time! Two birds, one step

### Step 6 - Set up a peering connection

In this step, I will Set up a connection link between your VPCs.

### Step 7 - Analyze flow logs

In this step, I will:
Review the flow logs recorded aboout VPC 1's public subnet.

Analyse the flow logs to get some tasty insights 👀

---

## Connectivity troubleshooting

My first ping test between my EC2 instances had no replies, which means the there was an issue witht he security group of vpc2, which i resolved asap.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-monitoring_99d4ba42)

I could receive ping replies if I ran the ping test using the other instance's public IP address, which means... there is a connection bw vpc1 and vpc2, which we had set up using vpc peering.

---

## Connectivity troubleshooting

Looking at VPC 1's route table, I identified that the ping test with Instance 2's private address failed because there was no inbound rule in the vpc2's subnet.

### To solve this, I set up a peering connection between my VPCs

I also updated both VPCs' route tables so that the traffic will route through the vpc peering thingy which i have set up.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-monitoring_7316a13d)

---

## Connectivity troubleshooting

I received ping replies from Instance 2's private IP address! This means we have established qa successful connection bw both the vpcs.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-monitoring_4ec7821f)

---

## Analyzing flow logs

Flow logs tell us about our networking activity.

For example, you might find one that says REJECT OK instead of ACCEPT OK at the end. These would represent the ping messages that failed to reach Instance 2!

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-monitoring_d116818e)

---

## Logs Insights

Logs Insights is a cloudwatch feature used to analyse logs.

I ran the query. The query "Top 10 byte transfers by source and destination IP addresses" is all about discovering the top 10 biggest data transfers between IP addresses in your network! You'll find out which resources are moving the most data, which uncovers the busiest traffic routes in your network.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-monitoring_3e1e79a1)

---

---
