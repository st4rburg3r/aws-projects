<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Encrypt Data with AWS KMS

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-kms)

**Author:** Trupti Vibhute  
**Email:** trupti.v19625@gmail.com

---

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-kms_w0x1y2z3)

---

## Introducing Today's Project!

In this project, I will demonstrate:
🔑 Create encryption keys with AWS KMS (Key Management Service).

🗄️ Encrypt a DynamoDB database with a KMS key.

➕ Add and retrieve data from your database to test your encryption.

🕵️‍♀️ Observe how AWS stops unauthorized access to your data.

💎 Give a user encryption access.


### Tools and concepts

Services I used include AWS key management service, DynamoDB and IAM. Key concepts I learnt include encryption giving key access to users, encrypting the database contents.

### Project reflection

This project took me approximately 30 mins... 

I chose to do this project today because wanted to learn more about the security in aws... S

---

## Encryption and KMS

ncryption is a process that uses algorithms to convert data into a secure format called ciphertext. Only authorised users can decrypt and restore the data to its original, readable state. Otherwise, it looks like a scrambled piece of text like bihtueg34509ua!

Software developers use encryption to secure user data, transactions, files and more.

In fact, many apps, websites, and devices use encryption behind the scenes. When you visit a site with "https" in the URL, your connection is encrypted. When you upload files to a cloud storage service like S3 or Google Drive, the service automatically encrypts your data. When you're having a call over Zoom or WhatsApp, the platform is also using encryption to protect your audio and video.

AWS Key Management Service (KMS) is a secure vault for your encryption keys. You use KMS to create, manage, and use encryption keys that protect the data in your AWS resources.

Encryption keys are broadly categorized as symmetric and asymmetric.. Symmetric encryption use a single encryption key to both lock (encrypt) and unlock (decrypt) your data. They are generally faster and more efficient for encrypting large amounts of data, which is why we're using one for our DynamoDB table. 

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-kms_a2b3c4d5)

---

## Encrypting Data

My encryption key will safeguard data in DynamoDB, which is one of AWS's database services. DynamoDB stands out as a fast and flexible way to store your data, which makes it a great choice for applications that need quick access to large volumes of data e.g. games.

The different encryption options in DynamoDB include... Owned by Amazon DynamoDB: Amazon DynamoDB fully manages the key, so you have no access or visibility to the key. Great for basic encryption where you don't need any control.



AWS managed key: AWS Key Management Service (KMS) manages the key, so it's not a customer managed key like what we created! You can see the key and its usage, but management is done by AWS.



Stored in your account, and owned and managed by you: aka a customer managed key (CMK). You create and manage the key in KMS, giving you full control. This is the most secure option and the one we're using in this project

I slected owned and managed by you.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-kms_q8r9s0t1)

---

## Data Visibility

With the access denial information, the key administrator can understand which permissions are missing for your user, and adjust the key's IAM policies! That's what we're doing in the secret mission...

Even though the data is encrypted, you as a user have permissions to use the encryption key in KMS.

DynamoDB is designed to decrypt the data on your behalf. When data is requested by an authorized user (like you) or an authorized application, DynamoDB retrieves the encrypted data, decrypts it with the key, then shows you the decrypted format so you can use it instantly. This security feature is called transparent data encryption.

Transparent data encryption makes sure that your data is secure at rest, yet still accessible to authorized users that have the right permissions.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-kms_c0d1e2f3)

---

## Denying Access

I configured a new IAM user which has complete access to dynamodb... 

After accessing the DynamoDB table as the test user, I encountered an error as The new IAM user i was logged in as (nextwork-kms-user) does not have the permission to decrypt the data.

Since the DynamoDB table is encrypted with a specific AWS KMS key, and your user does not have permission to use this key, the system prevents access for data security.. because... This confirmed...

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-kms_w0x1y2z3)

---

## EXTRA: Granting Access

To let my test user use the encryption key, I added a new user to the key users list My key's policy was updated.

Using the test user, I retried accessing the dynamodb and the intems in it.... I observed that it no more showed me an error.. which confirmed that i have successfully added this user to the list which allows to access to the database.

Other access controls, like security groups or permission policies, control access to a resource (e.g. a DynamoDB table) or an entire service (e.g. DynamoDB).

However, these don't protect the actual data within the resource, like the items inside a DynamoDB table. Once someone has access, they can see all the data they’re allowed to. These controls don’t prevent someone with access from reading or misusing the data.

If you use KMS encryption, you secure the data within the resource. Even if someone bypasses your access controls (like hacking into a server or intercepting data), they can’t understand the data unless they have the decryption key.

This adds a layer of security - only users with access permissions and decryption keys can view the actual data.

![Image](http://learn.nextwork.org/appreciative_brown_zany_lemon/uploads/aws-security-kms_feffb2fb8)

---

---
