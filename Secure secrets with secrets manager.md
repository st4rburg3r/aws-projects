<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Secure Secrets with Secrets Manager

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-secretsmanager)

**Author:** Trupti Vibhute  
**Email:** trupti.v19625@gmail.com

---

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-secretsmanager_r7s8t9u0)

---

## Introducing Today's Project!

In this project:
In 🔎 Step #1, we'll take a look at a simple web app that lists S3 buckets, clone it to our computer, and set it up to hardcode AWS credentials.
In 🍴 Step #2, we'll see what happens when we share this code (with the credentials hardcoded!) publicly on GitHub.
In 🔒 Step #3, we'll secure the credentials using AWS Secrets Manager.
In 📝 Step #4, we'll update the web app code to use the credentials from Secrets Manager.
In ⬆️ Step #5, we'll try share the code on GitHub again, and see how you can wipe your repository clean of all the hardcoded credentials!

### Tools and concepts

Services I used were AWS secrets manager, Github, IAM... 

### Project reflection

This project took me approximately 1.5 hours... The most challenging part was resolving the merge conflicts.

I chose to do this project today because i wanted to learn more about clous security.

---

## Hardcoding credentials

Exposing your AWS credentials publicly is a major security risk and is extremely unsafe for production applications. Once someone else gets access to your credentials, they can use them to access your AWS account, delete resources, steal data, and cause damage.

It's not just AWS credentials; database passwords, API keys for other services, and any kind of secret should never be directly embedded in your code.

These are example access keys for AWS - we're going to imagine that these are real AWS credentials that would give someone access to your AWS account!

We're using these test credentials as it's easier and safer to use than real credentials that would expose your account to security risks. Because these credentials are fake, putting them in config.py won't actually let your web app work (you won't see this web app display your S3 buckets' names).

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-secretsmanager_j2k3l4m5)

---

## Using my own AWS credentials

to set up my virtual environment, I installed all the neessary packages required for this by typing this command :
pip3 install -r requirements.txt 
and press Enter.

Damn - we got an error again! Guess that didn't work :(
Check the JSON response in your browser
This time, it's a JSON response saying {"error":"An error occurred (InvalidAccessKeyId)..."}.

This error means the AWS Access Key ID provided for the web app is not valid. Our app is running, but it can't access your AWS account because it doesn't have valid credentials!

This is because we are using the placeholder credentials in config.py, which are not real AWS credentials.

To resolve the 'InvalidAccessKeyId' error, I updated the config.py file with my original AWS credentials.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-secretsmanager_wghjteykut)

---

## Pushing Insecure Code to GitHub

Once I updated the web app code with credentials, I forked the repository.
When you fork a repository, you're making a copy of it in your GitHub account online. If your forked repository is public, anyone can see it!
When you clone a repository, you're creating a local, offline copy. By default, no one can see it since it's stored on your computer.

To connect my local repository to the forked repository, I entered the following commands in my terminal:
git init
Then I used git add and git commit to add and commit those changes. Finally, git push uploads all the changes made to the forked repository.

GitHub automatically scans your code for secrets and blocks the push if it detects any, like AWS credentials.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-secretsmanager_o2p3q4r5)

---

## Secrets Manager

AWS Secrets Manager is a service that helps you securely store and manage secrets, such as database credentials, API keys, and other sensitive information. Think of it as a digital vault for your secrets.

Secrets Manager encrypts your secrets and allows you to retrieve them programmatically in your applications, without hardcoding them in your code. It also offers features like secret rotation and auditing to further enhance security.

Secret rotation is the process of automatically changing your secrets on a regular schedule. This is a security best practice because it reduces the risk of compromised credentials. If a secret is compromised, it will only be valid for a limited time before it's automatically rotated.

Secret rotation is best for high-risk credentials like database passwords, privileged API keys, and service account credentials. These types of secrets, if compromised, could give attackers access to sensitive data or critical systems, so regular rotation helps limit the damage window.

This sample code is very helpful! It shows you exactly how to retrieve your secret from Secrets Manager in your application code. We'll use this code to update our config.py file.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-secretsmanager_h2i3j4k5)

---

## Updating the web app code

i updated the config.py file to use Secrets Manager instead of hardcoded credentials.

These lines are responsible for actually retrieving the credentials from the secret and assigning them to the AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, and AWS_REGION variables that our app.py code expects:
secret_json = json.loads(get_secret()): This line calls the get_secret() function to retrieve the secret from Secrets Manager. The secret is returned as a JSON string, so we use json.loads() to parse it into a Python dictionary.
AWS_ACCESS_KEY_ID = secret_json['AWS_ACCESS_KEY_ID']: This line extracts the value of the AWS_ACCESS_KEY_ID key from the secret_json dictionary and assigns it to the AWS_ACCESS_KEY_ID variable.
AWS_SECRET_ACCESS_KEY = secret_json['AWS_SECRET_ACCESS_KEY']: This line does the same for the AWS_SECRET_ACCESS_KEY.
AWS_REGION = region_name: This line sets the AWS_REGION variable to the region_name we defined earlier.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-secretsmanager_v0w1x2y3)

---

## Rebasing the repository

git rebase starts a rebase session, which means rewriting your commit history.
This is how we'll erase the commit containing the sensitive credentials. Use this command with caution, as rewriting history can cause issues like merge conflicts (which you'll see in just a second).

Open the config.py file in your code editor or terminal.
Delete the entire section between <<<<<<< HEAD and ======= (this removes the hardcoded credentials)
Then, at the end of the file, delete the ======= line
Delete the >>>>>>> feature-branch line
Save the file

Once the merge conflict was resolved, I verified that my  hardcoded credentials are out of sight in the repository by checking the config.py file.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-secretsmanager_t5u6v7w8)

---

---
