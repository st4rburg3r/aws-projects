<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Traffic Flow and Security

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-security)

**Author:** Trupti Vibhute  
**Email:** trupti.v19625@gmail.com

---

## VPC Traffic Flow and Security

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-security_92b0b0b4)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is your own private network inside AWS and it is useful because Your resources are isolated from others, it is scalaboe and we get to design the entire network.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create and learn abut Route Tables, Security Groups and Network Access Control Lists

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was the time it took to complete. soo many key concepts I covered in this project so it took a little longer.

### This project took me...

This project took me around 1.5 hrs. Took my time to understand each and every concept.

---

## Route tables

Route tables are basically a table of rules- called routes. It directs the traffic between the subnets and to the internet gateway.
They are responsible for connecting the resources to the internet.

Routes tables are needed to make a subnet public because route table has a route that directs all the internet bound traffic to the internet gateway. This is what makes the subnet public.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-security_0a07b191)

---

## Route destination and target

Routes are defined by their destination and target.
Destination is the ip range that the traffic wants to reach whereas the target is the path that the traffic with follow to reach the destination.

The route in my route table that directed internet-bound traffic to my internet gateway had a destination of 0.0.0.0/0 .... and the target was my internet gateway which i had ceated earlier

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-security_0a07b191)

---

## Security groups

Security groups control traffic on the resource level. Tey are stateful and remember the inbound and outbound traffic. Every resource must be associated with a security group

### Inbound vs Outbound rules

Inbound rules define the traffic which is allowed to reach the resources... I  configured an inbound rule that all http traffic on port 80, from any ip address is allowed.

Outbound rules are for the traffic that is exiting the subnet or the security group... By default, AWS security groups already allow all outbound traffic. So unless you specify otherwise, any resource associated with the security group can access and send data to any IP address - whether it's in your VPC, other VPCs (if you have the right permissions) and on the public internet!

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-security_92b0b0b4)

---

## Network ACLs

Network ACLs are list of rules for all the traffic entering and exiting the sublet. It is stateless and works at a subnet level.

### Security groups vs. network ACLs

Network ACLs are used to set broad traffic rules that apply to an entire subnet. For example, blocking incoming traffic from a particular range of IP addresses or denying all outbound traffic to certain ports.



Security groups allow for more granular control, managing access to individual resource. You can specify which ports and protocols are allowed for each connected resource.



---

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

By default, a network ACL's inbound and outbound rules will allow all the traffic.

In contrast, a custom ACL’s inbound and outbound rules are automatically set to deny all the traffic.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-security_4faeb056)

---

## Tracking VPC Resources

EC2 Global View is a tool  that lets you see and manage your EC2 and VPC resources across all AWS Regions from a single dashboard. Instead of switching between Regions to track your resources, this view gives you a single view at everything you have running, which is super useful for multi-region deployments.

Now that I've learnt about EC2 Global View, I'd use it again to see in which region my resources ae running.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-security_b03ea6162)

---

---
