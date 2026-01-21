<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Testing VPC Connectivity

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-connectivity)

**Author:** Eric Gitau  
**Email:** gitaueric09@gmail.com
 
---

## Testing VPC Connectivity

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-connectivity_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a secure, isolated section of the AWS cloud where you can launch and manage resources such as servers, databases, and applications. It gives you full control over your network setup, including IP addressing, subnets, route tables, security groups, and network ACLs.

It is useful because it allows you to design your own virtual network environment in the cloud, similar to how you would in a traditional on-premises data center. With a VPC, you can control inbound and outbound traffic, isolate sensitive workloads in private subnets, connect securely to the internet or on-premises networks, and scale resources as needed all while maintaining security and flexibility.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to set up core VPC components with the VPC wizard, launched EC2 instances, and tested the connectivity between my network resources. This hands-on exercise helped me understand how the different components such as subnets, route tables, internet gateways, and security groups work together to enable secure and reliable communication within a cloud environment.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was how small misconfigurations in security groups or network ACLs could completely block connectivity between resources. Even though my VPC and EC2 instances were set up correctly, missing a single rule meant my servers couldn’t communicate as intended. This experience taught me the importance of carefully reviewing security settings and understanding how each networking component contributes to successful connectivity.

### This project took me...

This project took me about 1 hour to complete. Within that time, I was able to design the VPC using the wizard, launch EC2 instances, configure networking components, and test connectivity between resources. The process was fast-paced but very insightful, showing me how much can be achieved in a short time with the right focus and understanding of AWS networking fundamentals.

---

## Connecting to an EC2 Instance

Connectivity in cloud networking means the ability of resources (like EC2 instances, databases, or servers) to communicate with each other or with the internet. It depends on proper configuration of components such as subnets, route tables, internet gateways, NAT gateways, security groups, and network ACLs. In short, connectivity is about making sure the right resources can talk to each other securely while blocking unwanted access.

My first connectivity test was to check whether I could successfully connect to my network’s public server (an EC2 instance). This test was important because it validated that my internet gateway, route tables, and security group rules were correctly configured. By confirming this connection, I ensured that the foundational setup of my VPC allowed secure and reliable access to resources in the public subnet.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

I connected to my EC2 instance using EC2 Instance Connect, a tool provided by Amazon EC2 that allows direct access to an instance through the AWS Management Console. With this method, I didn’t need to manage SSH key pairs manually, which simplified the process and improved security. This approach is especially useful for quick, browser-based access to instances while still maintaining controlled and temporary access.

My first attempt at getting direct access to the public server resulted in an error. After troubleshooting, I discovered that the issue was caused by the security group configuration of my private server it only allowed HTTP traffic and not SSH traffic, which runs on a different protocol. This highlighted the importance of configuring security groups correctly to match the type of access required, since even small misconfigurations can block connectivity.

I fixed this error by updating my private server’s security group to include a new inbound rule that allows SSH traffic from anywhere. This change enabled me to successfully establish a secure connection to the server. Through this step, I learned how adjusting security group rules directly impacts connectivity and how important it is to align inbound rules with the exact protocol required for access.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

Ping is a basic network utility used to test whether one device can reach another over a network. It works by sending small packets of data (ICMP requests) to a target IP address and waiting for a response. In my project, I used the command ping 10.0.0.74 to test the connectivity between my servers. This helped me verify that the network configuration allowed communication between instances inside the VPC.

The ping command I ran was ping 10.0.0.74. This command sent ICMP requests to the private server’s IP address to test connectivity. By running this test, I could verify whether traffic from my public server was successfully reaching the private server inside the VPC.

The first ping test returned no reply from my private server. This indicated that the security settings on the private server were blocking ICMP traffic (both inbound and outbound), which is the traffic type used by the ping command to check connectivity. This issue highlighted how network restrictions at the security group or NACL level can silently block communication even when the servers themselves are running correctly.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

I troubleshooted this issue by enabling ICMP traffic in both my private server’s security group and network ACL. As an additional step, I also verified that the source was correctly defined to point to the public subnet, ensuring that the communication path was properly configured. After making these changes, my ping command successfully returned replies, confirming that connectivity between the servers was working as expected.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

cURL is a connectivity tool that tests communication from one server to another and can also retrieve data. It works by sending requests over protocols such as HTTP or HTTPS, making it especially useful for checking whether a web server is accessible and responding correctly. Unlike ping, which only checks if a server is reachable, cURL provides actual responses from the target server, allowing deeper troubleshooting and validation of services.

I used cURL to test the connectivity between my network’s public server and the public internet. This test was successful only because my internet gateway, security group, and route table were set up correctly. Running cURL allowed me to confirm that my instance could not only reach the internet but also retrieve data, proving that all the networking components were properly configured and working together.

### Ping vs Curl

Ping and cURL are different because they test connectivity in different ways.

a) Ping checks basic network reachability by sending ICMP packets to a target IP address. If you get replies, it means the server is reachable over the network.

b) cURL, on the other hand, goes a step further by sending application-level requests (like HTTP or HTTPS) and retrieving actual data from the server. This helps verify not just that the server is reachable, but also that the specific service (e.g., a web app) is running and responding correctly.

In short: Ping tests if the door is open, while cURL checks what’s actually inside.

---

## Connectivity to the Internet

I ran the command
curl https://learn.nextwork.org/projects/aws-host-a-website-on-s3
and it successfully returned the HTML data for the NextWork first project page. This confirmed that my server could connect to the public internet, retrieve web content, and that my networking setup (internet gateway, route tables, and security groups) was working correctly. Using cURL in this way not only validated connectivity but also demonstrated how I can interact with real web applications directly from my instance.

![Image](http://learn.nextwork.org/inspired_purple_vibrant_plum/uploads/aws-networks-connectivity_8ee57662)

---

---
