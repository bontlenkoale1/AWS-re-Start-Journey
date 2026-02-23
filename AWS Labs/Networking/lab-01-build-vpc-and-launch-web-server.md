# Internet Protocols - Public and Private IP Addresses 🌐

---

## Lab Overview & Objectives 🎯

In this lab, I will:
- ✅ Summarize and investigate the customer scenario
- ✅ Analyze the difference between a private and public IP address
- ✅ Develop a solution to the customer's issue
- ✅ Summarize and describe my findings

---

## Customer Scenario 📧

 **My Role:** Cloud Support Engineer at Amazon Web Services (AWS)

During my shift, a customer from a Fortune 500 company requested assistance regarding a networking issue within their AWS infrastructure.

### Ticket from Customer:

```
Hello, Cloud Support!

We currently have one virtual private cloud (VPC) with a CIDR range of 10.0.0.0/16. 
In this VPC, we have two Amazon Elastic Compute Cloud (Amazon EC2) instances: 
instance A and instance B. Even though both are in the same subnet and have the 
same configurations with AWS resources, instance A cannot reach the internet, 
and instance B can reach the internet. I think it has something to do with the 
EC2 instances, but I'm not sure. I also had a question about using a public 
range of IP address such as 12.0.0.0/16 for a VPC that I would like to launch. 
Would that cause any issues? Attached is our architecture for reference.

Thanks!
Jess
Cloud Admin
```

### Customer Architecture:

*The customer's architecture consists of a VPC (10.0.0.0/16), an internet gateway, a public subnet containing both Instance A and Instance B.*


<img width="813" height="532" alt="vpc1 (1)" src="https://github.com/user-attachments/assets/b7ac257d-46a4-4cef-8ce2-067d0352047e" />




---

## Task 1️⃣: Investigate the Customer's Environment 🔍

When troubleshooting networking and AWS, I applied a troubleshooting method starting from the bottom and working my way up in layers using the OSI model as a reference.

### OSI Model vs. AWS Infrastructure:

| Layer | OSI Model | AWS Infrastructure |
|-------|-----------|---------------------|
| Layer 7 | Application | Application |
| Layer 6 | Presentation | Web Servers, application servers |
| Layer 5 | Session | EC2 instances |
| Layer 4 | Transport | Security group, NACL |
| Layer 3 | Network | Route Tables, IGW, Subnets |
| Layer 2 | Data Link | Route Tables, IGW, Subnets |
| Layer 1 | Physical | Regions, Availability Zones |

*This information is beneficial when troubleshooting network connectivity issues.*

In the AWS Management Console, I searched for and selected **EC2**.

In the left navigation menu, I chose **Instances**.

I copied the names and IP addresses of both instances for reference:

**Instance A Networking Information:**

| Attribute | Value |
|-----------|-------|
| Instance Name | Instance A |
| Private IPv4 Address | 10.0.0.10 |
| Public IPv4 Address | None |
| VPC | Lab VPC (10.0.0.0/16) |
| Subnet | Public Subnet |



<img width="1902" height="901" alt="Screenshot 2026-02-19 155300" src="https://github.com/user-attachments/assets/934bab7e-0030-42b6-be6a-cadee66ad265" />


**Instance B Networking Information:**

| Attribute | Value |
|-----------|-------|
| Instance Name | Instance B |
| Private IPv4 Address | 10.0.0.20 |
| Public IPv4 Address | 54.123.45.67 |
| VPC | Lab VPC (10.0.0.0/16) |
| Subnet | Public Subnet |



<img width="1906" height="918" alt="Screenshot 2026-02-19 155229" src="https://github.com/user-attachments/assets/f69fc43c-27f7-4f04-a60e-5640ae5c040a" />


### Key Observation:

**The critical difference:** Instance A has **only a private IP address** assigned, while Instance B has **both private and public IP addresses** assigned.

---
Task 2️⃣: Use SSH to Connect to EC2 Instances 🔌
For Windows Users:
I selected the Details drop-down menu above these instructions, then selected Show. A Credentials window was presented.

I selected the Download PPK button and saved the labsuser.ppk file to my Downloads directory.

I made a note of the PublicIP address for Instance B.

I downloaded and installed PuTTY from https://www.putty.org/

I opened putty.exe and configured my PuTTY session:

In the Host Name field, I entered: ec2-user@<public-ip-address> (replacing with Instance B's public IP)

Under Connection > SSH > Auth, I clicked Browse and selected the labsuser.ppk file

I clicked Open to start the connection

I clicked Yes when prompted to trust the host
<img width="1523" height="735" alt="Screenshot 2026-02-19 155616" src="https://github.com/user-attachments/assets/98017d46-2855-4c62-8813-58e89b970444" />

<img width="907" height="585" alt="Screenshot 2026-02-19 155716" src="https://github.com/user-attachments/assets/f6283740-70be-4f8e-a671-51975415a162" />

---

## Task 3️⃣: Send the Response to the Customer (Group Activity) 💬

### My Response to Jess:

**Subject: RE: Networking Issue and VPC CIDR Question**

Hello Jess,

Thank you for reaching out to AWS Cloud Support. I've investigated both of your questions and have the following findings to share.

**Issue 1: Instance A Cannot Reach the Internet**

After examining your architecture, I identified the root cause of the connectivity issue:

**Instance A does not have a public IP address assigned to it.** While both instances are in the same subnet with identical configurations, only Instance B has a public IP address. Private IP addresses (like the one assigned to Instance A) are designed for internal communication within your VPC and cannot be accessed from or communicate directly with the internet.

This was confirmed by attempting to SSH into both instances:
- Instance A (private IP only): Connection failed
- Instance B (public IP): Connection successful

**Solution:** To resolve this, you can:
1. Associate an Elastic IP address with Instance A, or
2. Configure the subnet to automatically assign public IP addresses to new instances

This will give Instance A the public-facing address it needs for internet connectivity.

**Issue 2: Using Public CIDR Range (12.0.0.0/16) for a New VPC**

**I strongly recommend against using public IP address ranges for your VPC.** Here's why:

1. **Routing Conflicts:** The IP range 12.0.0.0/16 is publicly owned by another organization (AT&T). If your VPC uses this range and you need to communicate with resources on the actual internet using that range, your traffic would be routed internally within your VPC instead of reaching the actual destination.

2. **No Internet Access:** Resources using public IP ranges within your VPC would not be able to reach the internet because AWS would treat those addresses as local to your VPC.

3. **RFC 1918 Compliance:** AWS VPCs are designed to work with private IP ranges as defined in **RFC 1918** (`10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`). These ranges are reserved for private networks and guaranteed not to conflict with public internet addresses.

**Best Practice:** Always use private IP ranges from RFC 1918 for your VPCs. For the new VPC you'd like to launch, I recommend using a CIDR block like `10.1.0.0/16` or `172.31.0.0/16`.

Please let me know if you'd like assistance implementing these solutions or have any additional questions.

Best regards,
Bridgette 
AWS Cloud Support Engineer

---

## Key Takeaways 💡

### Public vs. Private IP Addresses:

| Attribute | Private IP Address | Public IP Address |
|-----------|-------------------|-------------------|
| **Routability** | Within VPC only | Internet-wide |
| **Uniqueness** | Can be reused across VPCs | Globally unique |
| **Access** | Cannot be accessed from internet | Can be accessed from anywhere |
| **Cost** | Free | May incur charges (Elastic IP) |
| **RFC 1918** | Follows private ranges | Any non-RFC 1918 range |

### VPC CIDR Best Practices:

| Do ✅ | Don't ❌ |
|------|---------|
| Use RFC 1918 private ranges | Use public IP ranges owned by others |
| Plan for future growth | Use overlapping CIDRs with connected networks |
| Document your IP allocation | Use the same CIDR across multiple VPCs needing connectivity |

### Troubleshooting Methodology:

I applied a layered approach to troubleshooting:
1. Started at the bottom (EC2 instance layer)
2. Checked IP address assignments
3. Verified network connectivity
4. Escalated through OSI model layers as needed

---

## Important Notes ⚠️

- **Private IP Addresses:** Cannot be accessed from outside the VPC
- **Public IP Addresses:** Required for internet connectivity
- **RFC 1918:** Always use these ranges for VPC CIDR blocks
- **Public CIDR Risks:** Using public ranges can cause routing conflicts and connectivity issues
- **Auto-assign Public IP:** Can be enabled at subnet level for automatic public IP assignment

---

## Conclusion 🎉

I have now successfully:

- ✅ Investigated the customer's environment and identified the root cause
- ✅ Analyzed the difference between private and public IP addresses
- ✅ Developed a solution for the customer's internet connectivity issue
- ✅ Provided guidance on VPC CIDR best practices
- ✅ Communicated findings in a clear, professional manner

**Root Cause Summary:** Instance A lacked a public IP address, preventing internet access. The customer should always use private RFC 1918 ranges for VPC CIDR blocks to avoid routing conflicts.

---

## Additional Resources 📚

- [Amazon EC2 Instance IP Addressing](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html)
- [VPC CIDR Blocks](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-cidr-blocks.html)
- [RFC 1918 - Private Address Space](https://tools.ietf.org/html/rfc1918)
- [Connecting to Your Linux Instance Using SSH](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)
- [Elastic IP Addresses](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)

---
