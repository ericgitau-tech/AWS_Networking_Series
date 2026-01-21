<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Monitoring with Flow Logs

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-monitoring)

**Author:** Eric Gitau  
**Email:** gitaueric09@gmail.com
 
---

## VPC Monitoring with Flow Logs

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-monitoring_3e1e79a1)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon **VPC (Virtual Private Cloud)** is a private, isolated section of the AWS cloud where you can launch and manage your own resources, such as EC2 instances, databases, and load balancers. It is useful because it gives you full control over your networking environment—including IP address ranges, subnets, route tables, and security settings—so you can design it to meet your application’s needs. By completing today’s project, I learned how to **monitor traffic within a VPC using Flow Logs and CloudWatch**, which is essential for troubleshooting, ensuring security, and understanding network behavior.


### How I used Amazon VPC in this project

In today’s project, I used **Amazon VPC** to create two private networks, connect them with peering, and monitor their traffic using **Flow Logs** and **CloudWatch**. This allowed me to practice setting up networking, testing connectivity, and analyzing traffic patterns for troubleshooting and security.


### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was how much **troubleshooting is involved in getting VPC peering and routing to work correctly**. At first, I assumed the instances would communicate as soon as the peering connection was created, but I quickly learned that updating route tables and checking security rules is just as important. This gave me a deeper appreciation of how AWS networking works in practice.


### This project took me...

This project took me about **1 and a half hours** to complete. During that time, I was able to set up two VPCs, configure subnets, launch EC2 instances, establish a VPC peering connection, update route tables, enable Flow Logs, and analyze the captured traffic in CloudWatch. It was a hands-on experience that not only strengthened my understanding of AWS networking but also gave me practical skills in monitoring and troubleshooting VPC traffic.


---

## In the first part of my project...

### Step 1 - Set up VPCs

In this step, I will set up two VPCs from scratch. While network monitoring can be done with a single VPC, adding a second one introduces the extra challenge of configuring **VPC peering**. This is valuable because it allows me to monitor traffic not only within a single VPC but also across peered VPCs, giving me deeper hands-on experience with real-world networking scenarios.


### Step 2 - Launch EC2 instances

In this step, I will be launching two EC2 instances in each VPC. This is important for setting up the remainder of the project, as the instances will act as resources that can communicate with each other and generate network traffic. The traffic between these instances will be captured in **VPC Flow Logs**, which we will then monitor and analyze. This setup ensures there is real activity to track, making the monitoring process more meaningful and practical.


### Step 3 - Set up Logs

In this step, I will be setting up **VPC Flow Logs** to start monitoring network traffic. I am also configuring a storage destination for these logs, because Flow Logs need a place to store and organize the captured traffic data. By sending them to a storage service such as Amazon CloudWatch Logs or S3, I can easily access, analyze, and visualize the information. This makes it possible to track traffic patterns, troubleshoot issues, and gain insights into the security and performance of my VPCs.


### Step 4 - Set IAM permissions for Logs

In this step, I will provide **VPC Flow Logs** with the necessary permissions to create and upload logs into **CloudWatch Logs**. This is important because Flow Logs themselves don’t have permission to write data; they rely on an IAM role or resource policy that grants access. By giving these permissions, I ensure that the captured network traffic data can be delivered securely into my CloudWatch log group, where I can store, analyze, and visualize it for monitoring and troubleshooting.


---

## Multi-VPC Architecture

I started my project by launching two VPCs and creating two public subnets one in each VPC. At this stage, I did not include any private subnets, as the focus is on setting up basic connectivity and preparing the environment for monitoring and VPC peering.


The CIDR blocks for VPC 1 and VPC 2 are **10.1.0.0/16** and **10.2.0.0/16** respectively. These ranges must be unique, because if both VPCs shared overlapping IP addresses, it could cause routing conflicts and traffic failures when communicating between them. By using distinct CIDR blocks, I ensure smooth connectivity and avoid network issues during VPC peering and traffic flow.


### I also launched EC2 instances in each subnet

My EC2 instances’ security groups allow **SSH** and **ICMP** traffic. This is because we need SSH access to log into and manage the EC2 instances, and we allow ICMP traffic (such as ping) to perform connectivity tests between the instances and across VPCs. These rules make it possible to both administer the servers and generate the network traffic required for monitoring with Flow Logs.


![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-monitoring_e7fa8775)

---

## Logs

Logs in AWS are like a **big folder** where you store related information about your resources and their activities. For example, when you enable VPC Flow Logs, all the network traffic data is written into this “folder,” making it easy to organize, search, and analyze. Just like a physical folder keeps related documents together, AWS logs keep related events together so you can quickly track performance, detect issues, and monitor security.


**Log groups** in AWS are like labeled folders that organize your logs. Each log group contains one or more **log streams** (which are sequences of log events from a specific resource, like an EC2 instance). For example, you might have a log group called *VPC-Flow-Logs*, and inside it, you’ll find multiple log streams for different network interfaces. This structure helps keep logs tidy and makes it easier to manage, search, and analyze them in CloudWatch.


### I also set up a flow log for VPC 1

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-monitoring_e8398869)

---

## IAM Policy and Roles

I created an **IAM policy** because it lets me define rules that grant permissions to specific services or resources. In this case, the policy allows the **VPC Flow Logs service** to create log streams and upload log data into **CloudWatch Logs**. Without this policy, Flow Logs would not have the required access to deliver traffic data, so creating and attaching it ensures smooth log collection and monitoring.


I also created an IAM role because AWS services like VPC Flow Logs cannot directly use JSON policies on their own they must assume a role that has the required permissions. By creating and attaching this role, I provide VPC Flow Logs with the access it needs to record network traffic data and upload the logs into CloudWatch. This step is necessary to securely link the permissions defined in the IAM policy with the VPC Flow Logs service.

A **custom trust policy** is a special type of IAM policy that defines **who or what can assume a specific IAM role**. Unlike permission policies (which define *what actions* are allowed), a trust policy focuses on *who is trusted* to use the role. For example, in the case of VPC Flow Logs, the trust policy specifies that the **VPC Flow Logs service** is allowed to assume the IAM role so it can write logs into CloudWatch on our behalf.


![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-monitoring_4334d777)

---

## In the second part of my project...

### Step 5 - Ping testing and troubleshooting

In this step, I will be generating **network traffic**, which is important when learning about cloud networking and cloud engineering. With the Flow Logs already set up, the next step is to test if they can actually capture activity. To do this, I’ll have an instance in **VPC 1** try to communicate with an instance in **VPC 2**. This not only generates traffic for monitoring but also serves as a test of the **VPC peering** configuration. In other words, I’m achieving two goals at once—verifying that Flow Logs are working and confirming that VPC peering is properly set up—because both rely on successful communication between the instances.


### Step 6 - Set up a peering connection

In this step, I will set up a **VPC peering connection** so that VPC 1 and VPC 2 can communicate directly with each other. This is necessary because, by default, VPCs are isolated networks with no built-in connectivity between them. A peering connection acts as a secure bridge that allows resources in both VPCs to send traffic back and forth using their private IP addresses, enabling smoother communication and more realistic network monitoring.


### Step 7 - Analyze flow logs

In this step, I will be **extracting and analyzing the Flow Logs data** collected from our VPCs. This is important because Flow Logs capture detailed information about network traffic, such as source and destination IPs, ports, protocols, and whether the traffic was accepted or rejected. By analyzing this data, I can gain insights into connectivity patterns, troubleshoot issues, verify that traffic is flowing correctly through the VPC peering connection, and identify any unusual or potentially unauthorized activity.


---

## Connectivity troubleshooting

My first ping test between the EC2 instances had no replies, which indicates that something is blocking the ICMP traffic. This could be due to **security group rules**, **network ACLs**, or even a **routing issue** where the traffic is not being sent along the correct path. Identifying and fixing these kinds of issues is a normal part of testing connectivity, and troubleshooting them will help ensure both VPC peering and Flow Logs are working as expected.


![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-monitoring_99d4ba42)

I was able to receive ping replies when I ran the test using the other instance’s **public IP address**. This shows that the second instance is correctly allowing **ICMP traffic** from the outside. However, since the private IP test failed earlier, the issue is likely with the **VPC peering setup, routing tables, or private security rules**, rather than the instance itself blocking ICMP.


---

## Connectivity troubleshooting

Looking at VPC 1’s route table, I found that the ping test to Instance 2’s private address failed because there is no route configured to direct traffic from one VPC to the other. Without this route, packets sent to the other VPC’s CIDR block have nowhere to go, so the communication fails. Adding the correct route to point traffic through the VPC peering connection will fix this issue.


### To solve this, I set up a peering connection between my VPCs

I also updated both VPCs’ route tables so that any traffic destined for the other VPC’s CIDR block is routed through the **VPC peering connection** instead of being sent to the public internet. This allows instances in each VPC to reach the other VPC’s **IPv4 private addresses** directly. As a result, communication now stays private, secure, and efficient—exactly what we need for proper connectivity and accurate monitoring with Flow Logs.


![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-monitoring_7316a13d)

---

## Connectivity troubleshooting

I received ping replies from Instance 2's private IP address! This means setting up a peering connection and the route table so that connectivity erro of our vpc traffic not being able to navigatefrom one vpc to anaother

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-monitoring_4ec7821f)

---

## Analyzing flow logs

Flow Logs tell us details about the **source and destination** of network traffic, the **amount of data transferred**, and whether the traffic was **accepted or rejected** by security rules. They don’t show the actual content of the traffic, but they provide enough metadata to understand how your network is being used, spot performance issues, and detect possible security problems.


For example, my Flow Log shows **rejected traffic** from external IPs trying to reach my EC2 instance’s private IP (`10.1.8.22`). The action field shows `REJECT`, meaning the traffic was blocked by security groups or NACLs. In simple terms, random internet traffic was denied access—this is normal and confirms that my security rules and Flow Logs are working correctly.


![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-monitoring_d116818e)

---

## Logs Insights

**Logs Insights** is a specialized tool within Amazon CloudWatch that helps analyze logs using queries. It allows you to quickly search, filter, and extract useful information from large volumes of log data. You can also use it to create **visual graphs and charts** based on your queries, making it easier to spot patterns, troubleshoot issues, and monitor trends in your applications and network traffic.


I ran the query to **return the top 10 byte transfers by source and destination IP addresses**. This query analyzes the Flow Logs to identify which IP pairs are responsible for the largest amount of data transfer. By doing this, I can quickly see the most active connections in my VPC, understand traffic patterns, and spot potential anomalies such as unusually high data transfers that may need further investigation.


![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-monitoring_3e1e79a1)

---

---
