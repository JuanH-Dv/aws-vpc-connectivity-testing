<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Testing VPC Connectivity

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-connectivity)

**Author:** Juan Hernández  
**Email:** juanm.h.t@outlook.com

---

## Testing VPC Connectivity

![Image](http://learn.nextwork.org/thoughtful_azure_glamorous_nectarine/uploads/aws-networks-connectivity_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a virtual private cloud that lets users launch AWS resources in a logically isolated network. It is useful because it provides enhanced security, control over network configuration, and the ability to define custom routing and subnet structures.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a logically isolated network for my AWS resources. I set up a VPC with public and private subnets to demonstrate network segmentation. I launched EC2 instances in these subnets to test connectivity between them and to the internet. By configuring security groups and network ACLs, I controlled traffic flow within the VPC. This allowed me to verify that my public server could communicate with my private server and access the internet.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was having to update the security group for the NextWork Public Server to allow SSH traffic, enabling a connection via EC2 Instance Connect.

### This project took me...

This project took me about an hour.

---

## Connecting to an EC2 Instance

Connectivity means how well different parts of a network communicate with each other and with external networks.

My first connectivity test was whether I could connect to my public server.

![Image](http://learn.nextwork.org/thoughtful_azure_glamorous_nectarine/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

I connected to my EC2 instance using EC2 Instance Connect, which is a shortcut way to get direct SSH access to my EC2 instance through the AWS Management Console.

My first attempt at getting direct access to my public server resulted in an error, because the security group associated with NextWork Public Server only allows inbound HTTP traffic, but I was trying to connect using EC2 Instance Connect.

I fixed this error by updating the security group for NextWork Public Server to allow SSH traffic. I added an inbound rule with the Type set to SSH and selected "Anywhere-IPv4" as the source.

![Image](http://learn.nextwork.org/thoughtful_azure_glamorous_nectarine/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

Ping is a network tool that sends a small packet of data to a specific IP address. I used ping to test the connectivity between my NextWork Public Server and NextWork Private Server. This helped me verify that my EC2 instances could communicate with each other within my VPC setup.

The ping command I ran was: ping 10.0.1.133

The first ping returned a single line indicating that my Public Server sent out a ping message, but I didn't receive any replies back. This meant there was a connectivity problem between my NextWork Public Server and NextWork Private Server.

![Image](http://learn.nextwork.org/thoughtful_azure_glamorous_nectarine/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

I troubleshooted this by investigating the Network ACL and security group settings for my NextWork Private Server. I discovered that the Network ACL was blocking all inbound and outbound traffic, preventing ICMP messages from entering the private subnet. I fixed this by adding an inbound rule (Rule 100) to allow All ICMP - IPv4 traffic from my public subnet (10.0.0.0/24), and applied the same rule to outbound traffic. Then, I updated the NextWork Private Security Group to allow ICMP traffic from the NextWork Public Security Group.

![Image](http://learn.nextwork.org/thoughtful_azure_glamorous_nectarine/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

Curl is is a tool to test connectivity in a network. It sends HTTP requests to web servers to fetch data, such as HTML pages. 

I used curl to test the connectivity between my Public Sever instance and the internet.

### Ping vs Curl

Ping and curl are different because ping sends a small packet of data to check if a computer or device is reachable and measures the response time, while curl transfers data to or from a server. 

---

## Connectivity to the Internet

I ran the curl command: curl https://learn.nextwork.org/projects/aws-host-a-website-on-s3 
which returned the complete HTML content of NextWork's web app.

![Image](http://learn.nextwork.org/thoughtful_azure_glamorous_nectarine/uploads/aws-networks-connectivity_8ee57662)

---

---

---