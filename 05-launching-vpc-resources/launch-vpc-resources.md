<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launching VPC Resources

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-ec2)

**Author:** Eric Gitau  
**Email:** gitaueric09@gmail.com

---
 
## Launching VPC Resources

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-ec2_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a virtual network dedicated to your AWS account, where you can launch AWS resources like EC2 instances in isolated, customizable subnets.

It is useful because it gives you full control over networking, including IP address ranges, route tables, security groups, and network ACLs. This allows you to securely isolate resources, manage traffic flow, and build scalable cloud architectures tailored to your applications.

### How I used Amazon VPC in this project

I used Amazon VPC to create a secure and organized network environment for my AWS resources. This included setting up public and private subnets, route tables, security groups, and network ACLs, which allowed me to launch EC2 instances safely, control traffic flow, and understand how cloud networking works in a real-world scenario.

### One thing I didn't expect in this project was...

I didn’t expect how quickly the VPC Wizard could set up an entire network while still giving me the flexibility to customize resources. It was surprising to see how much manual networking knowledge I could apply even when using automated tools.

### This project took me...

This project took me aroud 45 min From setting up the VPC and subnets to launching both public and private EC2 instances, the entire process took approximately 1 hour. This hands-on experience helped me understand AWS networking concepts faster and reinforced best practices for secure cloud architecture.

---

## Setting Up Direct VM Access

Directly accessing a virtual machine means connecting straight into the operating system of your EC2 instance (like Linux or Windows) using a method such as SSH (for Linux) or RDP (for Windows). This gives you control of the VM’s environment, allowing you to install software, run commands, and configure the system just like you would on a physical computer.

### SSH is a key method for directly accessing a VM

SSH traffic means (Secure Shell) traffic is the encrypted network communication that happens when you connect securely to a Linux-based EC2 instance over port 22. It allows you to remotely log in and manage the instance’s operating system, run commands, and transfer files, all while keeping the connection secure from eavesdropping.

### To enable direct access, I set up key pairs

Key pairs are a set of security credentials that AWS uses to log in securely to an EC2 instance. They consist of a public key (stored in AWS) and a private key (downloaded and kept by you).

When you connect to an EC2 instance (for example, via SSH), AWS uses the key pair to verify your identity without requiring a password. This ensures secure, encrypted access to your instances.

The file format of a private key determines how it’s stored and used when connecting to an EC2 instance. AWS commonly provides private keys in the .pem (Privacy Enhanced Mail) format, which is used with OpenSSH on Linux and macOS. For Windows users, the key may need to be converted into a .ppk (PuTTY Private Key) format for use with PuTTY.

My private key’s file format was .pem, which allowed me to securely SSH into my EC2 instance from the terminal.

---

## Launching a public server

I had to change my EC2 instance's networking settings by modifying its subnet and security group rules so that it matched the design of my VPC. This involved ensuring the public EC2 instance was placed in the public subnet with access through the internet gateway, while the private EC2 instance was launched in the private subnet with no direct internet access. I also updated the security groups to allow only the necessary inbound and outbound traffic, and verified that the route tables were correctly configured to direct traffic through the proper gateways.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-ec2_88727bef)

---

## Launching a private server

My private server has its own dedicated security group because Each security group in AWS acts as a virtual firewall. By giving my private EC2 instance its own security group, I can apply custom inbound and outbound rules tailored only to that server. This ensures that it only accepts traffic from trusted sources (for example, my bastion host in the public subnet) and blocks all unnecessary access. Having a dedicated security group adds an extra layer of isolation and control, which is essential for protecting resources in a private subnet.

My private server’s security group’s source is set to the public EC2 instance’s security group, which means that only traffic coming from the bastion host can reach the private server. Instead of opening the private server to the entire internet or a wide IP range, this setup enforces a secure, controlled access path, allowing only trusted communication between the public and private layers of the VPC.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-ec2_4a9e8014)

---

## Speeding up VPC creation

I used an alternative way to set up an Amazon VPC! This time, I built the VPC using the VPC Wizard, which automated the creation of subnets, route tables, and gateways at a much faster pace. Compared to building everything manually, this approach saved time and showed me how AWS can simplify complex networking setups while still giving me the flexibility to customize resources afterward.

A VPC resource map is a visual representation of all the networking components inside a Virtual Private Cloud. It shows how resources such as subnets, route tables, internet gateways, NAT gateways, security groups, and EC2 instances are connected. This map helps you understand traffic flow, identify potential misconfigurations, and clearly see how public and private resources interact within your VPC.

My new VPC has a CIDR block of 10.0.0.0/16.
It is possible for my new VPC to have the same IPv4 CIDR block as my existing VPC because VPCs are isolated from each other within an AWS account. Each VPC maintains its own networking environment, so overlapping CIDR blocks don’t conflict unless I try to peer or connect the two VPCs. In that case, overlapping IP ranges would cause routing issues, and AWS would not allow the peering connection.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-ec2_1cbb1b88)

---

## Speeding up VPC creation

### Tips for using the VPC resource map

My new VPC has a CIDR block of 10.0.0.0/16.
It is possible for my new VPC to have the same IPv4 CIDR block as my existing VPC because VPCs are isolated from each other within an AWS account. Each VPC maintains its own networking environment, so overlapping CIDR blocks don’t conflict unless I try to peer or connect the two VPCs. In that case, overlapping IP ranges would cause routing issues, and AWS would not allow the peering connection.

The set up page also offered to create NAT gateways, which are NAT (Network Address Translation) Gateways are AWS-managed services that allow instances in private subnets to access the internet outbound (for software updates, patching, or API calls) while still preventing inbound connections from the internet. This is crucial in a VPC design because it lets private resources stay securely isolated while still being able to reach external services when needed.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-ec2_8ee57662)

---

---
