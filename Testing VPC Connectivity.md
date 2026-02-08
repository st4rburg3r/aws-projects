<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Testing VPC Connectivity

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-connectivity)

**Author:** Trupti Vibhute  
**Email:** trupti.v19625@gmail.com

---

## Testing VPC Connectivity

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-connectivity_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a private space for your cloud... and it is useful because... it seperatwes your resources from the entire cloud infrastructure.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to establish a connection between my public and private EC2  instance.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was getting sooooo many errors during the connecting part. But I resolved them all and completed the project with lots of learnings.

### This project took me...

This project took me 2 days because i couldnt figure out why the ping command wasnt giving any output.

---

## Connecting to an EC2 Instance

Connectivity is all about how well different parts of your network talk to each other and with external networks. It's essential because connectivity is how data flows smoothly across your network, powering everything from simple web hosting on the Internet to complex operations e.g. Netflix using over 100,000 EC2 instances to power its streaming platform. Solid connectivity is the backbone of any system that relies on network interactions, making every communication and operation reliable and efficient.

My first connectivity test was whether I could connect to the EC2 instance in my public subnet..

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

I connected to my EC2 instance using EC2 Instance Connect, which is an easier alternative of connecting to your EC@ server using ssh.

My first attempt at getting direct access to my public server resulted in an error, because there was no inbound rule in the public subnet security group. So I created a new inbound rule that allows ssh traffic to the instances, because we are trying to connect to our instance using the ssh protocol

I fixed this error by creating a new inbound rule in the public subnet security group.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

Ping is a common computer network tool used to check whether your computer can communicate with another computer or device on a network... I used ping to test the connectivity between... the public and private EC2 erver

The ping command I ran was ping 10.0.0.15

The first ping didnt not return any ping responses from the private server... This meant the private server was dropping the ping traffic.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

I troubleshooted this by adding proper rules in the NACLs and private security groups.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

Just like ping, curl is a tool to test connectivity in a network. Where ping checks if one computer can contact another (and how long messages take to travel back and forwth), curl is used to transfer data to or from a server. That means on top of checking connectivity, you can use curl to grab data from, or upload data into other servers on the internet!

I used curl to test the connectivity between my public EC2 instance and the internet

### Ping vs Curl

Ping and curl are different because ping just checks if the host is running or not. Curl alcually fetches the data

---

## Connectivity to the Internet

I ran the curl command curl example.com... which returned... me the contents of the web page in html.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-connectivity_8ee57662)

---

---
