<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Cloud Security with AWS IAM

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-iam)

**Author:** Trupti Vibhute  
**Email:** trupti.v19625@gmail.com

---

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-iam_1c864649)

---

## Introducing Today's Project!

### Project overview

In this project, I will demonstrate how to create an IAM user and make IAM policies to control access and permissions.. I'm doing this project to learn the basics of cloud security.

### Tools and concepts

Services I used were. amazon EC2 and AWs IAM .. Key concepts I learnt include... IAM users, policies, account aliases, policy simulator user groups, and how json policies work.

i also learned how to launce an instance, tqag an instance and also how to log in as an IAM user

### Project reflection

This project took me approximately 1.5 hrs.. The most challenging part was signing in as the IAM user and undestanding  the IAM policy as it was written in json and had multiple statements in it... It was most rewarding to see 'permission denied' when the intern tried to delete the production instance

---

## Tags

### What I did in this step

In this step, I will start with launching an ec2 instance ... because... we need some computing power.

### Understanding tags

 Tags are like labels you can attach to AWS resources for organization.

In this case, we're creating a tag called "Env" with a value of "production" or "development" to label the instances used in production vs development environments.

This tagging helps us with identifying all resources with the same tag at once (they are useful filters when you're searching for something), cost allocation, and applying policies based on environment types. You'll see the last point about policies in action soon!

### My tag configuration

The tag I’ve used on my EC2 instances is called. Name and env tag.. The value I’ve assigned for my instances are the ec2 instance name and the environment (development and production)

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-iam_2e0e5a5d)

---

## IAM Policies

### What I did in this step

In this step, I will be giving the omaginary intern the access to only developjment instance aqnd restrict accessing the4 production ec2 instance... because...We don't want them to accidentally shut down the platform or push their changes to the production environment while they're just testing things!

### Understanding IAM policies

An IAM policy is a rule for who can do what with your AWS resources. It's all about giving permissions to IAM users, groups, or roles, saying what they can or can't do on certain resources, and when those rules kick in.

### The policy I set up

You can create and edit AWS policies in the visual editor or JSON. In this project, we will use the JSON method.

### Policy effect

This policy allows some actions (like starting, stopping, and describing EC2 instances) for instances tagged with "Env = development" while denying the ability to create or delete tags for all instances.

### Understanding Effect, Action, and Resource

Extra for Experts: how are JSON policies structured?
Version
‍This means 2012-10-17 is the date of the latest policy version. This tells you whether the policy is up to date with the latest standards and practices.

‍Statement
‍The main part of the policy structure and defines a list of permissions.

‍Effect
‍This can have two values - either Allow or Deny - to indicate whether the policy allows or denies a certain action. Deny has priority. Looking at the first statement, "Effect": "Allow" means this statement is trying to allow for an action.

‍Action
‍A list of the actions that the policy allows or denies. In this case, "Action": "ec2:*" means all actions that you could possibly take on EC2 instances are allowed. Woohoo!

‍Resource
‍Which resources does this policy apply to? Specifying "*" means all resources within the defined scope (see the next point).

Condition Block (optional)
‍The circumstances under which the policy is in action. In this case, the condition is that the resou

---

## My JSON Policy

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-iam_1c864649)

---

## Account Alias

### What I did in this step

In this step, I will Simplify user login to your AWS account using an Account Alias

### Understanding account aliases

An account alias is An Account Alias is a friendly name for your AWS account that you can use instead of your account ID (which is usually a bunch of digits) to sign in to the AWS Management Console.

### Setting up my account alias

Creating an account alias took me 5 secs legit... 

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-iam_0eb4439b)

---

## IAM Users and User Groups

### What I did in this step

In this step, I will:
Set up a dedicated IAM group for all NextWork interns, so you can manage all interns' permissions from one place.

Set up a dedicated IAM user for your new intern, so they have a way to log in... 

### Understanding user groups

An IAM user group is a collection/folder of IAM users. It allows you to manage permissions for all the users in your group at the same time by attaching policies to the group rather than individual users.

### Attaching policies to user groups

I attached the policy I created to this user group, which means... all the users in this group will follow that policy (can only access development EC2 instance but not the production EC2 instance)

### Understanding IAM users

IAM users are peole or entities that hav access to your aws account

---

## Logging in as an IAM User

### Sharing sign-in details

The first way is  downloading the csv file and the swecond way is email the sign in instructions to the user

### Observations from the IAM user dashboard

Once I logged in as my IAM user, I noticed hat some of my dashboard panels are showing Access denied already.

... This was because of the iam user polices that i set

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-iam_6f2ab446)

---

## Testing IAM Policies

### What I did in this step

In this step, I will log in to aws using the dumy interns credentials an test access to the producctin and development instances to make sure the intern doesnt have the permision to accesss the production instance.

### Testing policy actions

I tested my JSON IAM policy by trying to delete both of the,. i couldnt delete the production instance as I was signed in as the intern ans wasnt allowed to access the production instance but was allowed to work, access and modify the development instance.

### Stopping the production instance

When I tried to stop the production instance i was met with a huge block of error code in red... This was because I (as an intern) wasnt allowed to do anything to the production instance as it was mentioned in the iam user policy

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-iam_0e7a9d6a)

### Stopping the development instance

Next, when I tried to stop the development instance., it was successfully stopped.. This was because the intern was allowed to make changes to the development instance

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-iam_1811801c)

---

## IAM Policy Simulator

To extend my project, I'm going to test the IAM user policies in a different way... I'm doing this because  testing the policies by deleting instances would be pretty disruptive for anyone whos working on them. so it's best practice to run these tests in another way. I am gonna  use a special IAM tool called the Policy Simulator to validate policies without affecting your actual AWS resources.

### Understanding the IAM Policy Simulator

The IAM Policy Simulator is. an alternative option to test your policies without actually deleting original elements .. It's useful for to validating policies without affecting your actual AWS resources.

### How I used the simulator

I set up a simulation to stop the development instance too... The results were.- It did actually stop it because the user group had the permission to make changes to only the development stage.. I had to specify the environment tag for this step

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-iam_069d8a621)

---

---
