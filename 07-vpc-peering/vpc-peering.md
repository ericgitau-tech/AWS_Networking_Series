<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-peering)

**Author:** Eric Gitau  
**Email:** gitaueric09@gmail.com
 
---

## VPC Peering

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a networking service that allows you to create and manage isolated virtual networks within AWS. It gives you full control over network settings such as IP address ranges, subnets, route tables, and gateways.

It is useful because it enables secure and scalable networking for your resources. In my project, I used Amazon VPC to set up a VPC peering connection, which allowed two VPCs to communicate privately using their internal IP addresses without exposing traffic to the public internet.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create two isolated virtual networks and establish a VPC peering connection between them. This setup allowed secure, private communication between EC2 instances in the two VPCs, enabling me to transfer data without exposing traffic to the public internet.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was the importance of properly configuring security groups and public IPs for EC2 instances. Even after setting up the VPC peering connection, I initially faced connection errors because the instances either lacked a public IPv4 address or did not allow ICMP/SSH traffic. This highlighted how critical it is to align networking and security settings when testing connectivity between VPCs.

### This project took me...

This project took me 1 hour to complete. During this time, I successfully created two VPCs, set up a VPC peering connection, configured route tables and security groups, launched EC2 instances, and verified connectivity between the VPCs. The hands-on experience helped me understand the practical steps and considerations required to enable secure, private communication in AWS.

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I will use the VPC Resource Map/Launch feature to quickly create two VPCs along with their essential components in just a few minutes. This approach simplifies the setup process by automatically provisioning key resources such as subnets, route tables, and gateways, allowing me to focus on configuring connectivity between the VPCs rather than manually building each component from scratch.

### Step 2 - Create a Peering Connection

In this step, I will create a VPC Peering Connection, which is a key VPC networking component. VPC peering allows two VPCs to communicate with each other using private IP addresses, without sending traffic over the public internet. This ensures secure, low-latency connectivity between the VPCs while maintaining isolation from external networks.

### Step 3 - Update Route Tables

In this step, I will edit the route tables for both VPC 1 and VPC 2 so that traffic can be directed through the VPC peering connection. By adding routes that point to the other VPC’s CIDR block with the peering connection as the target, I ensure that communication between the two VPCs is seamless and secure over the private network.

### Step 4 - Launch EC2 Instances

In this step, I will launch an EC2 instance in each VPC (VPC 1 and VPC 2). These instances will serve as test endpoints to verify the VPC peering connection. By connecting to the instances and running network tests (such as ping or SSH), I can confirm that traffic is successfully flowing between the two VPCs over the private peering link.

---

## Multi-VPC Architecture

I started my project by launching two VPCs, each with a unique CIDR block to avoid overlap and ensure proper routing. For simplicity, I configured each VPC with one public subnet, which will serve as the foundation for testing connectivity between the two environments.

The CIDR blocks for VPC 1 and VPC 2 were set to 10.1.0.0/16 and 10.2.0.0/16, respectively. It is important to assign unique CIDR ranges to each VPC to avoid IP address conflicts. Having distinct address spaces ensures that routing between the two VPCs works correctly and traffic can flow seamlessly across them.

### I also launched 2 EC2 instances

I did not set up key pairs for these EC2 instances because I am using EC2 Instance Connect to access them. This method allows secure, temporary SSH access without the need to manage or store private key files, making the connection process simpler and more secure.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC Peering Connection is a networking feature in AWS that enables two Virtual Private Clouds (VPCs) to communicate directly using private IP addresses. With peering, resources in both VPCs can send traffic to each other as if they were within the same network, without traversing the public internet. This provides a secure and efficient way to share data or applications between environments while keeping them logically isolated.

VPCs would use peering connections to share resources and enable private communication between different networks. For example, peering can allow applications in one VPC to access databases, file storage, or services hosted in another VPC without exposing the traffic to the public internet. This setup is often used to connect development and production environments, extend workloads across regions, or enable collaboration between different AWS accounts while maintaining security and isolation.

The difference between a Requester and an Accepter in a VPC peering connection is based on which VPC initiates the connection. The Requester VPC is the one that sends the peering connection request, while the Accepter VPC is the one that must approve the request. A peering connection becomes active only after the accepter confirms it. This two-step process ensures that both parties agree to establish the private link between their VPCs.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting the peering connection, I needed to update the route tables in both VPCs. This step is required because, by default, VPCs do not automatically know how to reach each other. By adding routes that point to the peering connection, each VPC’s route table can properly direct traffic destined for the other VPC’s CIDR block. Without these updates, the VPCs would remain isolated even though the peering connection is established.

My VPCs’ new routes have a destination of the other VPC’s CIDR block. The routes’ target was set to the VPC peering connection, ensuring that traffic from one VPC can be correctly directed to the other over the private link.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I will use EC2 Instance Connect to connect directly to the first EC2 instance. I am using this method because it provides secure, browser-based SSH access without requiring key pairs, and it allows me to quickly verify connectivity from within the AWS Management Console.

### Step 6 - Connect to EC2 Instance 1

In this step, I attempted to connect to the instance in VPC 1, but I encountered another error that prevented the use of EC2 Instance Connect directly:

“Failed to connect to your instance. Error establishing SSH connection to your instance. Try again later.”

This error occurred because the required inbound SSH (port 22) rule was missing from the instance’s security group. Without this rule, the connection request from EC2 Instance Connect could not reach the instance.

### Step 7 - Test VPC Peering

In this step, I will use the instance in VPC 1 to attempt a direct connection with the instance in VPC 2. This test is important because it validates that the VPC peering connection is set up correctly and that traffic can flow privately between the two VPCs. Successful communication confirms that the route tables, security groups, and peering configuration have been properly configured.

---

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to directly connect to the instance in VPC 1 through the AWS Management Console.

I was unable to use EC2 Instance Connect because the instance did not have a public IPv4 address assigned. For EC2 Instance Connect to work, the instance must have a public IP so that the SSH session can be established through the internet. Without it, the connection request cannot reach the instance.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, I set up Elastic IP addresses for my EC2 instances. Elastic IPs are static public IPv4 addresses that can be allocated and associated with an instance. By attaching an Elastic IP, the instance can be accessed securely from the internet, which enabled me to use EC2 Instance Connect without issues.

Associating an Elastic IP address resolved the error because it provided the EC2 instance with a public IPv4 address, which is required for EC2 Instance Connect. With the public IP assigned, the connection request from the AWS Management Console could reach the instance, allowing me to successfully establish an SSH session.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test the VPC peering connection, I ran a ping command to the private IPv4 address of the EC2 instance in VPC 2 (for example, ping 10.2.x.xxx). Using the private IP ensures that the traffic flows through the peering connection rather than the public internet, confirming that the setup is working as intended.

A successful ping test validated my VPC peering connection because it proved that traffic could flow privately between the two VPCs. If the peering connection had not been configured correctly, the ping request would not have received any reply from the other EC2 instance. This confirms that the route tables, security groups, and the peering setup were all functioning as expected.

I had to update the security group of my second EC2 instance because it was not allowing ICMP traffic, which is required for ping tests. To fix this, I added a new inbound rule that allows ICMP (Echo Request) traffic from the private CIDR block of the first VPC. This ensured that the instance in VPC 2 could receive and respond to ping requests coming from the instance in VPC 1.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-peering_7a29d352)

---

---
