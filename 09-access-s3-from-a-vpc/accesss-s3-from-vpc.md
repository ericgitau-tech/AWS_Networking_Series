<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Access S3 from a VPC

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-s3)

**Author:** Eric Gitau  
**Email:** gitaueric09@gmail.com 

---

## Access S3 from a VPC

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-s3_3e1e79a2)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a virtual network in AWS where you can launch and manage your resources, such as EC2 instances, databases, and load balancers. It is useful because it gives you full control over your networking environment, including IP address ranges, subnets, route tables, and security settings. With a VPC, you can securely connect your resources to the internet or keep them private, and control how they communicate with each other and with other AWS services.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to launch a VPC with a public subnet and deployed an EC2 instance inside it. I then directly accessed the instance and managed an Amazon S3 bucket through the AWS CLI on the EC2 instance. This setup allowed me to practice networking, compute, and storage integration in AWS.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was how quickly I could interact with Amazon S3 directly from my EC2 instance using the AWS CLI. It made me realize how powerful the command line is for managing AWS resources compared to always relying on the Management Console.

### This project took me...

This project took me about 1 hour to complete, including setting up the VPC, launching the EC2 instance, configuring the AWS CLI, and testing access to Amazon S3.

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I created a VPC with a public subnet. I then launched an EC2 instance inside the public subnet so that it can have direct internet access through an Internet Gateway. This makes it possible to securely connect to the instance via SSH and use it to access and interact with other AWS services, such as Amazon S3.

### Step 2 - Connect to my EC2 instance

In this step, I will directly access the EC2 instance using EC2 Instance Connect because it provides a secure, browser-based SSH connection without the need to manage or share SSH key pairs locally. This makes it easier to quickly log in to the instance and perform configurations while still following AWS best practices for security and access management.

### Step 3 - Set up access keys

In this step, I will create Access Keys because they allow my EC2 instance to securely access my AWS environment. With these keys, the instance can interact programmatically with AWS services, such as S3, without needing to log in through the AWS Management Console.

---

## Architecture set up

I started my project by creating a VPC and adding a public subnet to it. Inside this subnet, I launched an EC2 instance, which can be accessed over the internet through an Internet Gateway.

I also created an S3 bucket and uploaded two files into it. This setup allows my EC2 instance to later access the files, verifying that it has proper permissions to interact with AWS resources.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-s3_4334d777)

---

## Running CLI commands

AWS CLI (Command Line Interface) is a software tool that I can install on my local computer to manage and interact with AWS services directly from the terminal. It allows me to access and control my AWS account without always relying on the AWS Management Console.

In this project, I also have access to the AWS CLI because it comes pre-installed on the Amazon Linux EC2 instance, which means I can run AWS commands directly from the instance to interact with services like Amazon S3.

The first command I ran was `aws s3 ls`. This command is used to **list all the S3 buckets** in my AWS account or to **view the contents of a specific bucket** when a bucket name is provided. It helps verify that my EC2 instance has proper access to S3 and allows me to quickly check available storage resources and objects without using the AWS Management Console.


The second command I ran was `aws configure`. This command is used to **set up the AWS CLI with the necessary credentials and configuration**, including the **Access Key ID, Secret Access Key, default region, and output format**. It allows the CLI to authenticate with my AWS account and ensures that all subsequent commands can interact securely and correctly with AWS services.


![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-s3_e7fa8776)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I ran the aws configure command and provided my Access Key ID, Secret Access Key, a default region, and a default output format. This configuration allows the instance to authenticate with AWS and ensures that all future AWS CLI commands run smoothly.

**Access keys** are like a **username and password** for the AWS CLI or API. They allow you (or a program) to securely access your AWS account without logging into the AWS Management Console. Each access key has two parts: an **Access Key ID** (like a public username) and a **Secret Access Key** (like a private password), which together let AWS know that the requests you make come from you.


Secret Access Keys are like passwords for your Access Keys. They are used to authenticate and securely log in when your EC2 instance (or any application) interacts with AWS services through the CLI or API. Without the Secret Access Key, the Access Key alone cannot be used to access your AWS resources.

### Best practice

Although I’m using Access Keys in this project, a best practice is to use IAM Roles attached to the EC2 instance. This is more secure because it eliminates the need to store long-term credentials on the instance, and it allows you to easily attach or detach IAM policies to control permissions dynamically.

---

## In the second part of my project...

### Step 4 - Set up an S3 bucket

In this step, I will launch an Amazon S3 bucket and upload two files into it. This bucket will later be accessed by the EC2 instance to test whether the Access Keys have successfully granted the instance permission to interact with AWS resources. This helps verify that my instance can securely read from and write to S3.

### Step 5 - Connecting to my S3 bucket

In this step, I will use AWS CLI commands to control and manage my S3 bucket. This means I am interacting with the S3 bucket directly from the EC2 instance inside my VPC, instead of using the AWS Management Console. This approach is important because it helps me practice how developers and engineers often manage AWS resources programmatically, which is faster, automatable, and more secure than manual console operations.

---

## Connecting to my S3 bucket

The first command I ran was `aws s3 ls`. This command is used to **list all the S3 buckets** in my AWS account or to **view the contents of a specific bucket** when a bucket name is provided. It helps verify that my EC2 instance has proper access to S3 and allows me to quickly check available storage resources and objects without using the AWS Management Console.


When I ran the command aws s3 ls, the terminal responded with a list of my S3 buckets. This indicated that my Access Keys were configured correctly and that my EC2 instance has access to my AWS environment, allowing it to interact with S3.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-s3_4334d778)

---

## Connecting to my S3 bucket

Another CLI command I ran was
aws s3 ls s3://nextwork-vpc-project-eric2002,
which returned a list of the objects inside my S3 bucket. This confirmed that my EC2 instance could not only see the available buckets but also access the files stored inside a specific bucket.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-s3_4334d779)

---

## Uploading objects to S3

To upload a new file to my S3 bucket, I first ran the command:
sudo touch /tmp/test.txt

This command creates a blank file named test.txt inside the /tmp directory of my EC2 instance. The file will then be used for testing an upload to my S3 bucket.

The second command I ran was:
aws s3 cp /tmp/test.txt s3://nextwork-vpc-project-eric2002

This command uploads the blank file (test.txt) from my EC2 instance’s local /tmp directory to my S3 bucket (nextwork-vpc-project-eric2002). Running this verified that my EC2 instance could not only read from S3 but also write objects into the bucket.

The third command I ran was:
aws s3 ls s3://nextwork-vpc-project-eric2002

This validated that, by using my EC2 instance together with AWS CLI commands, I could successfully interact with another AWS service, in this case Amazon S3. The command listed the objects stored in my bucket, confirming that my instance had the right permissions to access S3.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-s3_3e1e79a2)

---

---
