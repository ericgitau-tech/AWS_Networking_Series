<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Endpoints

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-endpoints)

**Author:** Eric Gitau  
**Email:** gitaueric09@gmail.com

--- 

## VPC Endpoints

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-endpoints_09bcaa8a)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that lets you create a private, isolated network within the AWS cloud. It is useful because it allows you to control your network environment, including IP addresses, subnets, route tables, and security settings. With a VPC, you can securely launch and manage resources like EC2 instances and connect them safely to other AWS services without exposing them to the public internet.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to set up a VPC Endpoint, specifically an S3 Gateway. This provides my VPC with direct, private access to another AWS service (S3) without using the public internet, making the communication more secure and efficient.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was how important it is to correctly configure the route tables and policies. Even small misconfigurations could block access between my EC2 instance and S3, which helped me understand how network settings and security policies work together in AWS.

### This project took me...

This project took me 1 hour to complete, including setting up the VPC, EC2 instance, S3 bucket, configuring the VPC Endpoint, and testing access.

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I will set up the foundation of the project by launching a VPC, an EC2 instance, and an S3 bucket. These resources are needed so that I can later create and test the VPC Endpoint architecture. The VPC gives me a private network, the EC2 instance acts as a test server inside the VPC, and the S3 bucket is the storage service I want to connect to. With these in place, I will be able to test how the VPC Endpoint allows secure communication between the EC2 instance and S3 without using the public internet.

### Step 2 - Connect to EC2 instance

In this step, I will connect directly to my EC2 instance using EC2 Instance Connect. Connecting to the instance is important because it allows me to access the command line, run commands, and test communication with the S3 bucket.

### Step 3 - Set up access keys

In this step, I will set up an access key because my EC2 instance needs credentials to access the AWS environment. Without proper credentials, the instance cannot interact with AWS services like S3. Setting up the access key will allow the instance to run AWS CLI commands and communicate with resources in my account.

### Step 4 - Interact with S3 bucket

In this step, I will apply my access key credentials to the EC2 instance and then use the AWS CLI from the instance to access Amazon S3. This is necessary because the credentials authenticate the instance with AWS, allowing me to run commands and interact with the S3 bucket from within the EC2 environment.

---

## Architecture set up

I started my project by launching three key resources: a VPC, an EC2 instance, and an S3 bucket. These form the basic setup I need to later create and test the VPC Endpoint.

I also uploaded two files to my S3 bucket, which helped me test that my EC2 instance could successfully write data to the bucket through the VPC Endpoint.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-endpoints_4334d777)

---

## Access keys

### Credentials

To set up my EC2 instance so it can interact with the AWS environment, I configured it using the AWS Access Key ID, the matching Secret Access Key, the default region name, and the default output format. These settings allow the AWS CLI on the instance to authenticate and run commands against my AWS account.

Access keys are security credentials that an EC2 instance or any other server can use to access AWS services. They work like a username and password for the AWS CLI or SDKs. With access keys, a server can perform actions such as creating resources or reading information inside an AWS account. However, for security reasons, it is better to use IAM roles instead of long-term access keys, especially when working with EC2 instances.

Secret access keys are like a password in the context of AWS. When combined with the access key ID (like a username), they allow the EC2 instance (or any server) to authenticate and gain access to AWS services and the environment. This is why they must be kept safe and never shared.

### Best practice

Although I’m using access keys in this project, a best practice alternative is to use an IAM role. With an IAM role, the necessary permissions are attached to the role itself, and the role can then be associated with an EC2 instance or other resources. This provides secure, temporary access to AWS services without needing long-term access keys.

---

## Connecting to my S3 bucket

The first command I ran was aws s3 ls, which is used to list all the S3 buckets in my AWS account. However, the output showed an error message: “Unable to locate credentials. You can configure credentials by running aws configure.” This means that my EC2 instance did not yet have the proper IAM role or credentials set up to access S3, so the AWS CLI could not list any buckets.

The terminal responded with a list of my buckets. This indicated that the access keys I set up correctly gave my EC2 instance access to my AWS account and environment.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-endpoints_4334d778)

---

## Connecting to my S3 bucket

I also tested the command aws s3 ls s3://nextwork-vpc-project-eric144, which returned a list of the objects stored in the bucket. This confirmed that my EC2 instance could successfully access and read the contents of the S3 bucket using the AWS CLI.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-endpoints_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command sudo touch /tmp/nextwork.txt. This command creates an empty file named nextwork.txt and saves it locally in the /tmp directory of my EC2 instance. I later used this file to test uploading data to my S3 bucket.

The second command I ran was aws s3 cp /tmp/nextwork.txt s3://nextwork-vpc-project-eric144. This command copies the file I created (nextwork.txt) from my EC2 instance and uploads it into my S3 bucket. This confirmed that my EC2 instance had the correct permissions to write data to the bucket.

The third command I ran was aws s3 ls s3://nextwork-vpc-project-eric144, which validated that the new file (nextwork.txt) was successfully created and uploaded into my S3 bucket. Seeing the file listed in the bucket confirmed that the upload worked as expected.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-endpoints_3e1e79a2)

---

## In the second part of my project...

### Step 5 - Set up a Gateway

In this step, I will set up a VPC Endpoint so that communication between my VPC and AWS services like S3 is direct and more secure. Without a VPC Endpoint, traffic would normally go through the public internet. By using an endpoint, the traffic stays inside the AWS network, which reduces exposure and improves security.

### Step 6 - Bucket policies

In this step, I am going to restrict access to my S3 bucket so that only traffic coming from the VPC Endpoint can reach it. This means all other traffic from the public internet or other sources will be blocked, ensuring that only resources inside my VPC can access the bucket.

### Step 7 - Update route tables

In this step, I will test the connection between my EC2 instance and my S3 bucket through the VPC Endpoint. This is important because it confirms that the endpoint is working correctly and that my EC2 instance can securely access the bucket without using the public internet.

### Step 8 - Validate endpoint conection

In this step, I will validate my VPC Endpoint one more time. I will also use an endpoint policy to restrict my EC2 instance’s access to specific AWS resources. This is important because it ensures that even though the instance can access AWS services, it can only interact with the resources I allow, making the environment more secure and controlled.

---

## Setting up a Gateway

I set up an S3 Gateway, which is a type of VPC endpoint specifically designed for Amazon S3. The gateway works by updating the route table of the associated subnet so that any traffic bound for S3 goes through the gateway instead of the public internet. This allows my VPC to access S3 securely and directly.

### What are endpoints?

A VPC Endpoint is a component in a VPC that allows it to have a direct connection to AWS services like S3. This means that the traffic between the VPC and the service stays within the AWS network and does not have to go through the public internet, making it more secure and faster.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-endpoints_09bcaa8a)

---

## Bucket policies

A bucket policy is a type of policy that gives granular control over an S3 bucket. It defines who can access the bucket and what actions they are allowed to perform, such as reading, writing, or deleting objects. Using bucket policies helps make S3 access more secure and controlled.

My bucket policy is configured to deny traffic from all sources except for traffic coming from my VPC Endpoint. This ensures that only resources within my VPC can access the S3 bucket, making the communication more secure and preventing unauthorized access from the public internet.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-endpoints_7316a13d)

---

## Bucket policies

Right after saving my bucket policy, my S3 bucket page showed “Access Denied” warnings. This happened because the policy now blocks all traffic except from the VPC Endpoint, so any attempts to access the bucket from outside the VPC (including my own AWS console session) are denied. This confirms that the policy is working as intended.

I also had to update my route table because, by default, it did not provide a route for traffic in my public subnet to go through the VPC Endpoint. Adding this route ensures that any traffic from resources in the subnet destined for S3 is correctly directed through the endpoint instead of the public internet.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-endpoints_4ec7821f)

---

## Route table updates

To update my route table, I went to the Endpoints page in the VPC console and modified the route table from there. I associated it with my VPC public subnet, ensuring that traffic from the subnet destined for S3 goes through the VPC Endpoint instead of the internet.

After updating my public subnet’s route table, my EC2 instance was able to successfully connect to the S3 bucket. Access was no longer denied, confirming that traffic was correctly routed through the VPC Endpoint.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-endpoints_d116818e)

---

## Endpoint policies

An endpoint policy is a type of policy designed to specify which resources and actions are allowed through a VPC Endpoint. It controls what an endpoint can access and what operations can be performed, helping to enforce security and limit permissions for resources accessed via the endpoint.

I updated my endpoint policy by changing the effect from "Allow" to "Deny". I could see the effect immediately because when I tried to run another AWS S3 command from my EC2 instance, access to the S3 bucket was denied. This demonstrated that the endpoint policy correctly controlled which actions the instance could perform.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-endpoints_3e1e79a3)

---

---
