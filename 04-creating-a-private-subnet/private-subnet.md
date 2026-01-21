<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Creating a Private Subnet

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-private)

**Author:** Eric Gitau  
**Email:** gitaueric09@gmail.com

---

## Creating a Private Subnet

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project! 

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a logically isolated section of the AWS cloud where you can launch and manage resources inside your own defined network. It gives you full control over IP addressing, subnets, route tables, internet gateways, and security configurations. It is useful because it allows you to design secure, scalable, and highly available architectures isolating public-facing resources like web servers in public subnets while protecting sensitive workloads like databases and backends in private subnets, all within a controlled and customizable network environment.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to practice secure cloud networking by creating a private subnet to isolate sensitive resources from direct internet exposure, configuring a private route table to control traffic flow within the VPC and prevent unauthorized access, and implementing a custom private Network ACL to enforce stateless, subnet-level rules that tightly restrict inbound and outbound traffic. This setup demonstrates how different VPC components work together to build a secure, controlled, and production-ready network architecture in AWS.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project is how the default configurations (main route table and default NACL) allow more traffic than I initially realized. I had to explicitly create and associate custom route tables and network ACLs to enforce proper isolation for my private subnet. This helped me understand the importance of not relying on defaults in AWS and instead designing custom configurations to meet specific security requirements.

### This project took me...

This project took me around 45 minutes to complete, including setting up the private subnet, configuring the custom route table, and implementing the private Network ACL. The hands-on practice was a great way to strengthen my understanding of how AWS networking components work together to secure and isolate resources.

---

## Private vs Public Subnets

The difference between a public subnet and a private subnet is that a public subnet has a route to the internet through an Internet Gateway (IGW), allowing resources like web servers to be accessible from outside the VPC. In contrast, a private subnet does not have a direct route to the internet, making it ideal for hosting sensitive resources such as databases, backend applications, or internal services that should remain isolated from external access.

Having private subnets is useful because they provide an extra layer of security by ensuring that critical resources such as databases, backend applications, and authentication systems are not directly exposed to the internet. This isolation reduces the attack surface, enforces best practices for secure architecture, and allows controlled communication with other resources through NAT gateways, bastion hosts, or internal routing.

My private and public subnets cannot have the same CIDR block (IP address range) because each subnet within a VPC must use a unique range of IP addresses. Overlapping CIDR blocks would cause routing conflicts and prevent AWS from correctly assigning IPs to resources, which would break network communication. Defining distinct CIDR ranges ensures that traffic can be routed properly between subnets and across the VPC.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, my private subnet is associated with the main route table of the VPC, which typically does not provide a route to the Internet Gateway. To enforce proper isolation and traffic control, I need to explicitly create and associate a custom private route table with the subnet, ensuring that resources inside remain inaccessible from the internet while still being able to communicate securely with other parts of the network.

I had to set up a new route table because the default main route table applies to all subnets in the VPC by default, which can cause unintended traffic flows. By creating a custom private route table and explicitly associating it with my private subnet, I can precisely control how traffic is routed ensuring there’s no direct path to the Internet Gateway while still allowing secure communication within the VPC or through a NAT Gateway if outbound internet access is required.

My private subnet’s dedicated route table only has one inbound rule and one outbound rule that allow traffic within the VPC’s internal network. This means resources inside the private subnet can communicate securely with other subnets or services in the same VPC, but they cannot send or receive traffic directly from the internet. This controlled routing ensures that sensitive resources like databases or backend systems remain fully isolated and protected.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, my private subnet is associated with the default Network ACL that comes with every VPC. This default ACL allows all inbound and outbound traffic, which is not secure for hosting sensitive resources. To strengthen security, I created a custom private Network ACL with explicit rules to tightly control traffic flow at the subnet level, ensuring only the necessary communication is permitted.

I set up a dedicated Network ACL for my private subnet because the default ACL allows all traffic in and out, which is not secure for sensitive workloads. By creating a custom ACL, I can enforce stateless, subnet-level rules that explicitly allow only the required inbound and outbound traffic (such as internal VPC communication) while denying everything else. This provides an extra security layer on top of security groups, ensuring resources like databases and backend systems remain tightly controlled and isolated.

My new Network ACL has two simple rules — one inbound rule and one outbound rule — that only allow traffic within the VPC’s internal IP range while denying everything else. This setup ensures that resources in my private subnet can securely communicate with other subnets in the VPC but remain completely isolated from direct internet access, adding a strong layer of protection for sensitive workloads.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-private_1ed2cb07)

---

---
