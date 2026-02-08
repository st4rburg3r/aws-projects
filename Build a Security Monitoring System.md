<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Security Monitoring System

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-monitoring)

**Author:** Trupti Vibhute  
**Email:** trupti.v19625@gmail.com

---

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-monitoring_reghtjy)

---

## Introducing Today's Project!

In this project, I will demonstrate how to build your own powerful monitoring system using AWS. 

### Tools and concepts

Services I used were CLoud Watch, Cloud Trail, S3, Simpl messaging service,  Secrets manager,  ... Key concepts I learnt include how to se up an alert tto monitor literally anythong on your AWS account.

### Project reflection

This project took me approximately 2 hours... The most challenging part the torubleshooting i had to do to get the alert.... It was most rewarding to hear a ding notifocation from my mobile (it was the same alert i set up)

---

## Create a Secret

AWS Secrets Manager helps you protect secrets, which are passwords, API keys, credentials and sensitive information. Instead of storing important credentials in your code (yikes!) or sharing them via email (double yikes!), you can tuck them safely away in Secrets Manager.

To set up for my project, I created a secret called TopSecretInfo that contains the value- I need 3 coffees a day to function

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-monitoring_o5p6q7r8)

---

## Set Up CloudTrail

AWS CloudTrail is a monitoring service - think of it as an activity recorder throughout your AWS account. It documents every action taken, like who did what, when they did it, and where they did it from.

A trail tells CloudTrail exactly what activity to record and where to save those recordings. When you create a trail, you're essentially saying "Hey CloudTrail, please keep track of all xyz activities and store the data in this specific location."

CloudTrail captures different types of events, each showing you a different view into what's happening in your AWS account:

Management events: These show you admin actions that configure your AWS resources - creating an EC2 instance, updating a security group, or in our case, accessing a secret. We're focusing on these in our project since secret access gets recorded here.

Data events: These track high-volume actions that operate ON your resources rather than creating or configuring them - like uploading a file to S3 or running a Lambda function.

Insights events: These detect unusual patterns in your management events, like someone suddenly creating 100x more IAM users than normal.

Network activity events: These track network-related activities, like changes to your VPC configuration or traffic to a subnet.

### Read vs Write Activity

Read API activity happens when someone views but doesn't change anything. For example, listing your S3 buckets, describing your EC2 instances, or in our project, viewing (but not changing) metadata about a secret.

Write API activity occurs when changes happen - creating, deleting, modifying resources, or even retrieving the value of a secret (which is what we want to monitor).


---

## Verifying CloudTrail

I retrieved the secret in two ways: First through the secrets manager console... Second using... AWS cloudshell

To analyze my CloudTrail events, I visitedthe cloudtrail service -> events managr and filtered the events by seleting event name as the filter and typing GetSecretValue. I found. three events matching theis event name. This tells me someone tried to access the secret value three times.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-monitoring_s8t9u0v1)

---

## CloudWatch Metrics

CloudWatch Logs is a service that helps you bring together your logs from different AWS services, including CloudTrail, for visibility, troubleshooting, and analysis.

It's especially powerful because once your logs are in CloudWatch, you can create alerts based on specific patterns (such as someone accessing your secret), visualize trends, or trigger automated responses.

CloudWatch Logs is where we can set up alerts and automated responses when specific events happen, which we'll start setting up in this step.
CloudTrail Event History only keeps events for 90 days, while CloudWatch Logs can store them for as long as you'd like.



CloudWatch Logs has powerful filtering tools that let us focus on exactly the events we care about.

A CloudWatch metric is  What are CloudWatch metric filters?
Metric filters automatically scan through your logs looking for specific patterns. Instead of you manually reading thousands of log entries to find mentions of "GetSecretValue", a metric filter automatically detects these patterns and keeps count for you.

We're creating a filter to specifically detect when someone retrieves our secret's value, which is defined by the action "GetSecretValue".

Metric value is what gets recorded when our filter spots a match in the logs. We're setting it to 1 so that each time someone accesses our secret, the counter increases by exactly one.



Default value is what gets recorded when our filter doesn't find any matches during a given time period. We're setting it to 0 so that time periods with no secret access show up as zero on our charts, rather than not showing up at all. This gives us a complete picture - we can see both when access happened AND when it didn't.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-monitoring_a9b0c1d2)

---

## CloudWatch Alarm

A CloudWatch alarm is an autmateed tool n AWS which watches cloudwatch metrics and creates an alert if any event crosses the threshhold value.... I set my CloudWatch alarm threshold to 1... so the alarm will trigger when anyone tried to access the secret once or more than once.

I created an SNS topic along the way. An SNS topic is like a broadcast channel for your notifications and alerts where the emails who would be notified are the subscribers....

AWS requires email confirmation for SNS subscriptions primarily to prevent spam, verify ownership, and ensure users actually want to receive notifications, stopping unwanted messages by requiring a click on a confirmation link sent to the specified email address before messages are delivered, a crucial security step for Application-to-Person (A2P) communication. .

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-monitoring_fsdghstt)

---

## Troubleshooting Notification Errors

To test my monitoring system, I tried to access my secret once again . I was expenting an SNS message from CloudWatch as i had diisabled SNS through Cloudrtail

But i didnt et anyyyyy alet or notification!!

There are a few places in thte monitoring system where things could be breaking:

CloudTrail didn't record the GetSecretValue event.

CloudTrail isn't sending logs to CloudWatch.

CloudWatch's metric filter isn't filtering logs correctly.

CloudWatch's Alarm isn't triggering an action.

SNS isn't delivering emails to you.

I initially didn't receive an email before because maybe the alarm isnt being triggered when it should . ... 

I checked a few critical settings:
Head back to the CloudWatch console
Select All alarms from the left hand navigation panel.
Check the checkbox for your alarm.
Select the Actions dropdown, and select Edit.
On the alarm details page, look at the Statistic field.
Aha - maybe the statistic should be set to Sum, not Average or any other statistic!

This is crucial because:
Sum adds up all occurrences of secret access in the period (what we want).
Average would calculate an average rate (i.e. the average number of times our secret was accessed per second over the 5 minute period), which might never cross our threshold.

---

## Success!

To validate that my system works, i accessed the secret ultiple times due to which the alarm i created went off and i got the mail.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-monitoring_ageraergearge)

---

## Comparing CloudWatch with CloudTrail Notifications

In the project extension, I configured direct CloudTrail notifications and compared that against using CloudWatch and alarms. This challenge will build the critical thinking skills around how architecture decisions (like using CloudWatch) are made when building cloud solutions (like this monitoring system).

After enabling CloudTrail SNS notifications, my inbox was looded with the emails...
The huge wave of emails will continue to happen as long as you keep your trail's SNS notification setting on, and there is any activity in your account.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-monitoring_d7e8f9g0)

---

---
