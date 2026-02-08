<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launching VPC Resources

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-ec2)

**Author:** Trupti Vibhute  
**Email:** trupti.v19625@gmail.com

---

## Launching VPC Resources

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-ec2_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is basically your private space inside the cloud architecture ... and it is useful because it isolates you from the entire cloud

### How I used Amazon VPC in this project

I used Amazon VPC to create public and private instances in the subnets and also learned how to launch an entire VPC using the VPC resource map.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was  how easily we can create an entire VPC usint the VPC resource map.

### This project took me...

This project took me 30 minutes.

---

## Setting Up Direct VM Access

Directly accessing a virtual machine means direct;y logging into the server (EC2 instance) without logging i to AWS console.

### SSH is a key method for directly accessing a VM

SSH, or Secure Shell, is the protocol we use for this secure access to a remote machine. When you connect to the instance, SSH verifies you possess the correct private key corresponding to the public key on the server, ensuring only authorized users can access the instance.

### To enable direct access, I set up key pairs

Key pairs in AWS EC2 are how you prove you’re allowed to log in to a virtual server.
No password. No guessing. Just cryptography.

Just like how documents can be saved in various file formats like PDF, DOCX, or TXT, each suited for different applications or systems, private keys also come in different file formats. Not every system or application can process all these formats, so choosing the right one is crucial.

The .pem format, which stands for Privacy Enhanced Mail, started off as a way to secure emails but has since become the go-to format for managing cryptographic keys because it is supported by many different types of servers e.g. EC2 instances!

---

## Launching a public server

Start your response with 'I had to change my EC2 instance's networking settings by assigning the EC2 instance to the public subnet and the VPC. Then i also assigned it the public security group.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-ec2_88727bef)

---

## Launching a private server

My private server has its own dedicated security group becausewe do not want the same traffiic as the public subnet to enter our private subnet and access the EC2 instance deployed there.

Choosing the NextWork Public Security Group as the source means only resources that are part of the NextWork Public Security Group can communicate with your instance. This restricts access to a much smaller group of trusted resources, rather than allowing potentially any IP address on the internet (0.0.0.0/0) to access your instance. A great move for securing a private subnet!

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-ec2_4a9e8014)

---

## Speeding up VPC creation

I used an alternative way to set up an Amazon VPC! This time, I did it using the VPC Resource map.

A VPC resource map is an architectural layout of your entire VPC network.

It is possible for my new VPC to have the same IPv4 CIDR block as my existing VPC because they are not connected in any way. If they are connected using VPC peering, it would create a conflict.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-ec2_1cbb1b88)

---

## Speeding up VPC creation

### Tips for using the VPC resource map

This is AWS' best practice advice at work! When you pick 2 Availability Zones, the wizard makes sure you have a public subnet in each one. This way, your public resources stay up even if one of the two Availaiblity Zones goes down.

This setup is called redundancy (having backups in different places) and high availability (making sure your resources are always accessible). Just one public subnet wouldn’t offer this kind of reliability, so AWS doesn't let you create just one!



The set up page also offered to create NAT gateways, which are like internet gateways but for your private subnet. These are used only when resources from the private subnet have to access the interner for some updates or patches.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-networks-ec2_8ee57662)

---

---
