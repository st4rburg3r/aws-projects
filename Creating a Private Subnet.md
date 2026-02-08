<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Creating a Private Subnet

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-private)

**Author:** Trupti Vibhute  
**Email:** trupti.v19625@gmail.com

---

## Creating a Private Subnet

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is your own private netwrok inside cloud0... 

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create private subnet. private route table and at last, a private NACL.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project is it was wayyy too easy because i had already c reated public subneta.

### This project took me...

This project took me 10 minutes only.

---

## Private vs Public Subnets

The difference between public and private subnets is that public subnet contains all the information and resources which can be viewd and accessed by the internet.
this includes web servers etc.
Private subnet contains databases, private resources etc.

For example, it's very common for engineers to set up an EC2 instance hosting their web app in a public subnet, but keep the database of customers and login details in a private subnet.

Having private subnets are useful as a private subnet is used to host resources that should not be directly accessible from the internet, improving security and isolation.

My private and public subnets cannot have the same CIDR blocks because it will create a conflict. The traffic wont be directed towards a single subnet. Plus we dont want the internet to access the private subnet in any way.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, my private subnet is associated with the public route table

I had to set up a new route table because by defaulot my private subnet is associated with the public route table. 

My private subnet's dedicated route table only has one inbound and one outbound rule that allows only communication within the vpc. Any traffic going to an IP inside 10.0.0.0/16 stays inside the VPC.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, my private subnet is associated with the default NACL which allows ll the traffic.

I set up a dedicated network ACL for my private subnet because... relying only on route table configurations might not be great for security.

My new network ACL has two simple rules -denying both inbound and outbound traffic. Lets keep it that way for noe. We will change that later in the upcoming projects.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-private_1ed2cb07)

---

---
