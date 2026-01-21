<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Traffic Flow and Security

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-security)

**Author:** Eric Gitau  
**Email:** gitaueric09@gmail.com

---

## VPC Traffic Flow and Security 

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-security_92b0b0b4)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a logically isolated network environment within AWS where you can launch and manage your resources securely. It is useful because it gives you full control over your network configuration, including IP address ranges, subnets, route tables, and security settings, allowing you to design a secure and scalable cloud infrastructure.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create an isolated network environment, configure subnets, route tables, security groups, and network ACLs, and enable secure communication between resources as well as controlled access to the internet.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how critical proper route table and security group configurations are for enabling connectivity. Even small misconfigurations can block traffic, highlighting the importance of understanding VPC traffic flow and security rules in detail.

### This project took me...

This project took approximately 1hr to complete, including planning, creating the VPC components, configuring route tables, security groups, and network ACLs, and testing the network connectivity

---

## Route tables

Route tables are sets of rules, called routes, that determine how network traffic is directed within a VPC. They control the flow of traffic between subnets, the internet, and other networks, ensuring that packets reach their intended destinations.

Route tables are needed to make a subnet public because they define how traffic from the subnet is routed to the Internet Gateway. Without a route directing outbound traffic to the Internet Gateway, resources in the subnet cannot communicate with the internet, even if an Internet Gateway is attached to the VPC.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-security_0a07b191)

---

## Route destination and target

Routes are defined by their destination and target. The destination specifies the range of IP addresses the route applies to, while the target indicates where the traffic should be directed, such as a subnet, Internet Gateway, NAT Gateway, or peering connection.

The route in my route table that directs internet-bound traffic to my Internet Gateway has a destination of 0.0.0.0/0 (representing all IP addresses) and a target of my Internet Gateway ID (igw-xxxxxxxx).

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-security_0a07b191)

---

## Security groups

 Security groups are virtual firewalls that control inbound and outbound traffic for resources in a VPC. They operate at the instance level, allowing you to define rules that permit or deny specific types of network traffic, thereby securing your resources.

### Inbound vs Outbound rules

Inbound rules are the set of rules in a security group that control the traffic allowed into your resources. I configured an inbound rule that allows HTTP traffic on port 80 from any IP address, enabling web clients to access my application.

Outbound rules are the set of rules in a security group that control the traffic allowed to leave your resources. By default, my security group's outbound rule allows all traffic to any destination (0.0.0.0/0), enabling resources to initiate connections to the internet or other networks.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-security_92b0b0b4)

---

## Network ACLs

Network ACLs (Access Control Lists) are stateless virtual firewalls that control inbound and outbound traffic at the subnet level within a VPC. They allow or deny traffic based on rules, providing an additional layer of security alongside security groups.

### Security groups vs. network ACLs

The difference between a security group and a network ACL is that security groups are stateful and operate at the instance level, automatically allowing return traffic for inbound or outbound connections, while network ACLs are stateless and operate at the subnet level, requiring explicit rules for both inbound and outbound traffic.

---

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

By default, a network ACL's inbound and outbound rules allow all traffic. This means that unless you explicitly add rules to deny or restrict traffic, all inbound and outbound packets are permitted through the subnet.

In contrast, a custom Network ACL’s inbound and outbound rules are automatically set to deny all traffic. This means that no traffic is allowed until you explicitly add rules to permit specific inbound and outbound connections.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-security_4faeb056)

---

## Tracking VPC Resources

---

---
