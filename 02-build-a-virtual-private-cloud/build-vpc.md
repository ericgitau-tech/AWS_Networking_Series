<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Virtual Private Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-vpc)

**Author:** Eric Gitau  
**Email:** gitaueric09@gmail.com 

---

## Build a Virtual Private Cloud (VPC)

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-vpc_2facf927)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a Virtual Private Cloud that allows you to launch and manage AWS resources within it. It is useful because it provides a private, isolated network environment where you have full control over IP addressing, subnets, routing, and security.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to create an isolated virtual network where I could securely deploy and manage resources. I set up subnets, attached an Internet Gateway, and configured routing to enable communication between my VPC and the internet.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was realizing how important it is to configure route tables correctly without them, even resources with public IPs cannot access the internet.

### This project took me...

This project took me approximately 60 minutes to complete, including setting up the VPC, subnets, and Internet Gateway, and configuring the necessary routing.

---

## Virtual Private Clouds (VPCs)

VPCs are isolated virtual networks that allow me to deploy resources in a secure environment, ensuring that they are only accessible according to the access controls I define.

My AWS account already included a default VPC, which is automatically created when a new account is set up. The default VPC is provided to help beginners launch and use AWS resources immediately, without needing to first configure a custom VPC.

To set up my VPC, I had to define an IPv4 CIDR block, which specifies the range of private IP addresses that resources within the VPC can use.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-vpc_2facf927)

---

## Subnets

Subnets are subdivisions within a VPC that allow you to deploy resources sharing the same characteristics, such as security requirements or accessibility. In my AWS account, some default subnets already exist one in each Availability Zone so resources can be distributed across multiple zones for high availability.

Once I created my subnet, I enabled the auto-assign public IPv4 address setting. This ensures that any EC2 instance launched in the subnet automatically receives a public IP address, so it can communicate with the internet without requiring manual configuration.

The key difference between public and private subnets is internet accessibility. A public subnet has a route to the Internet Gateway, which allows resources within it to connect to the internet. In contrast, a private subnet has no such route, so its resources remain isolated from direct internet access.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-vpc_157c4219)

---

## Internet gateways

An Internet Gateway is like a door attached to a VPC that enables communication between the VPC and the internet, allowing resources in public subnets to send and receive traffic.

Attaching an Internet Gateway to a VPC allows the VPC to access the internet. Without this step, even EC2 instances with public IP addresses would be unreachable, making any applications hosted on those servers unavailable and preventing the VPC from communicating with the internet.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-vpc_4ae90410)

---

## Using the AWS CLI

VPC resources can also be created using AWS CloudShell, which is a browser-based shell environment provided by AWS. CloudShell gives you a pre-configured CLI environment without the need to install or configure anything locally. The AWS Command Line Interface (CLI), on the other hand, is a tool that allows you to interact with AWS services from your own terminal, giving you more flexibility and control, especially when automating tasks or integrating with scripts.

To set up a VPC or a subnet, you can use the aws ec2 commands in the AWS CLI. When doing so, it is important to include the --cidr-block parameter, which defines the IP address range for the VPC or subnet. Omitting this parameter will result in an error, since every VPC and subnet must have a valid CIDR block assigned.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-vpc_9b2465411)

---

---
