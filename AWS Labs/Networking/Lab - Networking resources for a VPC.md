# Creating Networking Resources in an Amazon Virtual Private Cloud (VPC) 🌐

---

## Lab Overview & Objectives 🎯

In this lab, I will:
- ✅ Summarize and investigate the customer scenario
- ✅ Create a VPC, Internet Gateway, Route Table, Security Group, Network Access Control List, and EC2 instance
- ✅ Familiarize myself with the AWS Management Console
- ✅ Develop a solution to the customer's networking issue
- ✅ Validate the solution by successfully pinging outside the VPC

---

## Customer Scenario 📧

**My Role:** Cloud Support Engineer at Amazon Web Services (AWS)

During my shift, a customer from a startup company requested assistance regarding a networking issue within their AWS infrastructure.

### Email from Customer:

```
Hello Cloud Support!

I previously reached out to you regarding help setting up my VPC. I thought 
I knew how to attach all the resources to make an internet connection, but 
I cannot even ping outside the VPC. All I need to do is ping! Can you please 
help me set up my VPC to where it has network connectivity and can ping? 
The architecture is below. Thanks!

Brock, startup owner
```

### Customer Architecture:

*The customer's architecture consists of a VPC with CIDR range 192.168.0.0/18, an Internet Gateway, a public subnet with CIDR range 192.168.1.0/26, and a security group around an EC2 instance.*


<img width="741" height="401" alt="vpc (3)" src="https://github.com/user-attachments/assets/51d8b660-34a5-4765-bf23-16f496072db9" />


---

## Task 1️⃣: Investigate the Customer's Needs 🔍

Before building the solution, I reviewed the core components needed for a VPC to have internet connectivity:

### VPC Networking Components Overview:

| Component | Purpose | Key Characteristic |
|-----------|---------|---------------------|
| **VPC** | Virtual data center in the cloud | Logically isolated network |
| **Private IP Address** | Internal communication within VPC | Cannot be accessed from internet |
| **Public IP Address** | Communication outside VPC | Required for internet access |
| **Internet Gateway (IGW)** | Enables internet connectivity | Performs NAT; target route: 0.0.0.0/0 |
| **Subnet** | Range of IP addresses within VPC | Public subnet for internet-facing resources |
| **Route Table** | Directs traffic using defined rules | Associate with subnet; contains routes |
| **Security Group** | Instance-level firewall | Stateful; blocks everything by default |
| **Network ACL** | Subnet-level firewall | Stateless; does not block everything by default |

### Troubleshooting Approach:

I applied a **top-down methodology** following the left navigation pane in the VPC console, starting from "Your VPCs" and working my way down through each component.

---

## Task 1 Steps: Building the VPC Infrastructure 🏗️

### Step 1: Access the AWS Console

1. Selected the **AWS** button in the top right of the Vocareum environment
2. Navigated to **VPC** under Recently visited services or via Services > Networking & Content Delivery > VPC


---

### Step 2: Create the VPC

1. In the left navigation pane, selected **Your VPCs**
2. Clicked **Create VPC** in the top right corner

**Configuration:**
| Field | Value |
|-------|-------|
| Name tag | Test VPC |
| IPv4 CIDR block | 192.168.0.0/18 |
| IPv6 CIDR block | No IPv6 CIDR block |
| Tenancy | Default |

<img width="1906" height="905" alt="Screenshot 2026-02-22 165829" src="https://github.com/user-attachments/assets/a46498ba-2a8c-4e10-8c07-d6e307cb3b42" />



3. Clicked **Create VPC**

<img width="1910" height="917" alt="Screenshot 2026-02-22 170001" src="https://github.com/user-attachments/assets/b0fb41dc-2888-4ef1-9684-b5fa7d7812f6" />


---

### Step 3: Create the Subnet

1. In the left navigation pane, selected **Subnets**
2. Clicked **Create subnet** in the top right corner

**Configuration:**
| Field | Value |
|-------|-------|
| VPC ID | Test VPC |
| Subnet name | Public subnet |
| Availability Zone | No preference |
| IPv4 CIDR block | 192.168.1.0/18 |


<img width="1911" height="917" alt="Screenshot 2026-02-22 170426" src="https://github.com/user-attachments/assets/0d129648-5e3f-4f8c-be04-4698391ab596" />


3. Clicked **Create subnet**


<img width="1910" height="922" alt="Screenshot 2026-02-22 172023" src="https://github.com/user-attachments/assets/0d3b9f4c-50c7-478d-b9d0-8703a08b766d" />



---

### Step 4: Create the Route Table

1. In the left navigation pane, selected **Route Tables**
2. Clicked **Create route table** in the top right corner

**Configuration:**
| Field | Value |
|-------|-------|
| Name | Public route table |
| VPC | Test VPC |

<img width="1917" height="917" alt="Screenshot 2026-02-22 172315" src="https://github.com/user-attachments/assets/0f6d626c-e637-40ed-9668-e2fb23a34af0" />


3. Clicked **Create route table**



<img width="1911" height="909" alt="Screenshot 2026-02-22 172351" src="https://github.com/user-attachments/assets/a1f46d2d-11b5-494a-a927-fcd240dedaca" />

---

### Step 5: Create and Attach Internet Gateway

1. In the left navigation pane, selected **Internet Gateways**
2. Clicked **Create internet gateway** in the top right corner

**Configuration:**
| Field | Value |
|-------|-------|
| Name tag | IGW test VPC |

3. Clicked **Create internet gateway**


4. After creation, clicked **Actions** > **Attach to VPC**
5. Selected **Test VPC** from the dropdown
6. Clicked **Attach internet gateway**

<img width="1911" height="909" alt="Screenshot 2026-02-22 172610" src="https://github.com/user-attachments/assets/41b6f2d4-77df-4343-9d78-bab5eaee4a7e" />

---

### Step 6: Add Route to Route Table and Associate Subnet

1. Navigated back to **Route Tables** in the left navigation pane
2. Selected **Public route table**
3. Scrolled to the bottom and selected the **Routes** tab
4. Clicked **Edit routes**

**Add Internet Gateway Route:**
| Field | Value |
|-------|-------|
| Destination | 0.0.0.0/0 |
| Target | Internet Gateway (IGW test VPC) |

5. Clicked **Save changes**

<img width="1918" height="913" alt="Screenshot 2026-02-22 172833" src="https://github.com/user-attachments/assets/646a20e8-8594-4ae3-a57b-708495c70e3a" />


6. Selected the **Subnet associations** tab
7. Clicked **Edit subnet associations**
8. Selected **Public subnet**
9. Clicked **Save associations**

<img width="1908" height="906" alt="Screenshot 2026-02-22 172949" src="https://github.com/user-attachments/assets/013df0c4-36f4-408b-97bb-6308366dbc10" />


---

### Step 7: Create Network ACL

1. In the left navigation pane, selected **Network ACLs**
2. Clicked **Create network ACL** in the top right corner

**Configuration:**
| Field | Value |
|-------|-------|
| Name | Public Subnet NACL |
| VPC | Test VPC |

<img width="1910" height="916" alt="Screenshot 2026-02-22 173110" src="https://github.com/user-attachments/assets/1bc1205e-2bd3-4b42-ad76-7f3f482630ec" />


3. Clicked **Create network ACL**


**Configure Inbound Rules:**
1. Selected **Public Subnet NACL** from the list
2. Selected the **Inbound rules** tab
3. Clicked **Edit inbound rules**
4. Clicked **Add new rule**

| Field | Value |
|-------|-------|
| Rule number | 100 |
| Type | All traffic |
| Protocol | All |
| Port range | All |
| Source | 0.0.0.0/0 |
| Allow/Deny | ALLOW |

5. Clicked **Save changes**



**Configure Outbound Rules:**
1. Selected the **Outbound rules** tab
2. Clicked **Edit outbound rules**
3. Clicked **Add new rule**

| Field | Value |
|-------|-------|
| Rule number | 100 |
| Type | All traffic |
| Protocol | All |
| Port range | All |
| Destination | 0.0.0.0/0 |
| Allow/Deny | ALLOW |

4. Clicked **Save changes**


**NACL Rule Interpretation:**
- **Inbound Rule 100:** Allows all traffic from any source (0.0.0.0/0) to enter the subnet
- **Outbound Rule 100:** Allows all traffic from the subnet to go to any destination
- **Asterisk (*):** Any traffic not matching these rules is automatically denied

---

### Step 8: Create Security Group

1. In the left navigation pane, selected **Security Groups**
2. Clicked **Create security group** in the top right corner

**Basic Details Configuration:**
| Field | Value |
|-------|-------|
| Security group name | public security group |
| Description | allows public access |
| VPC | Test VPC |


**Inbound Rules Configuration:**
| Type | Protocol | Port Range | Source | Description |
|------|----------|------------|--------|-------------|
| SSH | TCP | 22 | 0.0.0.0/0 | SSH access from anywhere |
| HTTP | TCP | 80 | 0.0.0.0/0 | Web traffic from anywhere |
| HTTPS | TCP | 443 | 0.0.0.0/0 | Secure web traffic from anywhere |



<img width="1910" height="916" alt="Screenshot 2026-02-22 173944" src="https://github.com/user-attachments/assets/b976979b-9f25-42e5-8d73-a4f9ed1e48bf" />
<img width="1908" height="870" alt="Screenshot 2026-02-22 174101" src="https://github.com/user-attachments/assets/b13737ed-3cd0-4f66-a40a-9e7644b351da" />


**Outbound Rules Configuration:**
| Type | Protocol | Port Range | Destination | Description |
|------|----------|------------|-------------|-------------|
| All traffic | All | All | 0.0.0.0/0 | Allow all outbound traffic |

<img width="1913" height="921" alt="Screenshot 2026-02-22 174012" src="https://github.com/user-attachments/assets/7a625609-3a6a-4204-9b8d-bb52d72bc054" />


3. Clicked **Create security group**


<img width="1908" height="870" alt="Screenshot 2026-02-22 174101" src="https://github.com/user-attachments/assets/1bf68f3a-736d-4f42-9b1f-e7b441752ac0" />

---

## Task 2️⃣: Launch and Connect to EC2 Instance 🚀

### Step 1: Launch EC2 Instance

1. In the AWS Management Console search bar, entered and selected **EC2**
2. In the left navigation pane, selected **Instances**
3. Clicked **Launch instances**

**Instance Configuration:**

| Section | Field | Value |
|---------|-------|-------|
| Name | Name | (left blank) |
| Application and OS Images | Quick Start | Amazon Linux |

<img width="1915" height="917" alt="Screenshot 2026-02-22 175136" src="https://github.com/user-attachments/assets/afefe5b6-ab3a-42cc-903d-7b19f4c34709" />


| | Amazon Machine Image | Amazon Linux 2023 AMI |
| Instance type | Instance type | t3.micro |
| Key pair | Key pair name | vockey |

<img width="1915" height="913" alt="Screenshot 2026-02-22 175156" src="https://github.com/user-attachments/assets/e736ef15-d42f-4095-b000-71e39f6eccf1" />


| Network settings | VPC | Test VPC |
| | Subnet | Public subnet |
| | Auto-assign public IP | Enable |
| Firewall (security groups) | | Select existing security group |
| | Existing security group | public security group |

<img width="1912" height="914" alt="Screenshot 2026-02-22 175212" src="https://github.com/user-attachments/assets/2398b136-8117-400d-b4d6-9ae3770b65e9" />

4. Clicked **Launch instance**
5. Clicked **View all instances** to monitor launch status



*The instance transitions from **Pending** to **Running** state.*

---

### Step 2: Connect to EC2 Instance via SSH

#### For Windows Users (PuTTY):

1. Selected the **Details** drop-down menu above these instructions
2. Selected **Show** to display Credentials window
3. Downloaded the **labsuser.ppk** file
4. Made note of the instance's **Public IP address**
5. Opened **PuTTY**
6. Configured session:
   - Host Name: `ec2-user@<public-ip-address>`
   - Connection > SSH > Auth: Browse and select `labsuser.ppk`
7. Clicked **Open**
8. Clicked **Yes** when prompted to trust the host
<img width="610" height="551" alt="Screenshot 2026-02-22 175829" src="https://github.com/user-attachments/assets/58996155-d731-4f49-803f-1ad0692f82ff" />


---

## Task 3️⃣: Test Internet Connectivity with Ping 📡

### Step 1: Run Ping Test

Once connected to the EC2 instance via SSH, I ran the following command:

```bash
ping google.com
```

<img width="1919" height="1019" alt="Screenshot 2026-02-22 180008" src="https://github.com/user-attachments/assets/116c3083-2558-4900-a760-e6aa13a60d31" />


### Step 2: Verify Successful Connectivity

**Expected Successful Ping Output:**
```
PING google.com (142.250.190.46) 56(84) bytes of data.
64 bytes from den03s10-in-f14.1e100.net (142.250.190.46): icmp_seq=1 ttl=105 time=12.3 ms
64 bytes from den03s10-in-f14.1e100.net (142.250.190.46): icmp_seq=2 ttl=105 time=11.8 ms
64 bytes from den03s10-in-f14.1e100.net (142.250.190.46): icmp_seq=3 ttl=105 time=12.1 ms
64 bytes from den03s10-in-f14.1e100.net (142.250.190.46): icmp_seq=4 ttl=105 time=11.9 ms
^C
--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 11.8/12.025/12.3/0.194 ms
```
<img width="1919" height="1017" alt="Screenshot 2026-02-22 180030" src="https://github.com/user-attachments/assets/f397ad2a-7da0-483e-910f-71a5af293e6b" />



### Step 3: Exit Ping

Pressed **CTRL+C** (Windows) or **CMD+C** (Mac) to stop the ping command.

**The successful ping responses with 0% packet loss confirmed that:**
- ✅ The VPC has internet connectivity
- ✅ The Internet Gateway is properly attached and configured
- ✅ The route table has the correct 0.0.0.0/0 route to the IGW
- ✅ The security group allows outbound traffic
- ✅ The network ACL allows both inbound and outbound traffic
- ✅ The subnet is properly associated with the route table
- ✅ The EC2 instance has a public IP address

---

## Task 4️⃣: Send Response to Customer (Group Activity) 💬

### My Response to Brock:

**Subject: RE: VPC Internet Connectivity Issue - Resolution Provided**

Hello Brock,

Thank you for reaching out to AWS Cloud Support. I've investigated your VPC configuration and have successfully built and tested a working solution that allows your EC2 instance to ping outside the VPC.

**Issue: VPC Resources Not Properly Configured for Internet Connectivity**

After reviewing your architecture, I identified that while you had the basic components (VPC, IGW, subnet, security group), they weren't fully configured to work together. Here's what was missing:

1. **Route Table Configuration:** The route table needed a route to the Internet Gateway (0.0.0.0/0 → IGW)
2. **Subnet Association:** The route table wasn't associated with your public subnet
3. **Network ACL Rules:** The default NACL needed explicit allow rules for all traffic
4. **Security Group Rules:** Inbound SSH, HTTP, and HTTPS rules needed to be added

**Solution Implemented:**

I've created a fully functional VPC with the following properly configured components:

| Component | Configuration | Purpose |
|-----------|--------------|---------|
| **VPC** | 192.168.0.0/18 | Your requested CIDR range |
| **Public Subnet** | 192.168.1.0/28 | Hosts internet-facing resources |
| **Internet Gateway** | Attached to VPC | Enables internet connectivity |
| **Route Table** | 0.0.0.0/0 → IGW | Routes internet-bound traffic |
| **Network ACL** | Allow all inbound/outbound | Subnet-level firewall |
| **Security Group** | Allow SSH, HTTP, HTTPS | Instance-level firewall |
| **EC2 Instance** | t3.micro with public IP | Tested connectivity |

**Verification Steps Performed:**

1. Launched an EC2 instance in the public subnet with auto-assign public IP enabled
2. Connected via SSH using the provided key pair
3. Ran `ping google.com` command
4. **Successfully received responses with 0% packet loss**

**Key Takeaways for Your Future VPC Deployments:**

✅ **Follow the left navigation pane** in order when building VPCs (VPC → Subnets → Route Tables → IGW → NACLs → Security Groups)

✅ **Always add the IGW route** (0.0.0.0/0) to your route table after creating and attaching the IGW

✅ **Associate your route table** with the appropriate subnet

✅ **Configure both inbound and outbound rules** for security groups and NACLs

✅ **Enable auto-assign public IP** for instances that need internet access

✅ **Test connectivity** with ping to validate your configuration

**Your Working Architecture:**

```
Internet
    ↑
    │
[Internet Gateway]
    ↑
    │ (0.0.0.0/0 route)
[Route Table] ← Associated with → [Public Subnet 192.168.1.0/28]
    ↑                                          ↑
    │                                          │
[Network ACL (Allow All)]              [EC2 Instance with Public IP]
    ↑                                          ↑
    │                                          │
[Security Group (SSH, HTTP, HTTPS)] ← Protected by
```

**Next Steps:**

1. You can now use this working configuration as a template for your production environment
2. Consider adding more restrictive security rules based on your specific needs
3. For enhanced security, you might want to limit SSH access to your office IP address instead of 0.0.0.0/0
4. Explore adding NAT Gateways for private subnets if needed

Please let me know if you'd like assistance implementing this solution in your environment or have any additional questions about VPC configuration.

Best regards,
Bridgette
AWS Cloud Support Engineer

---

## Solution Summary & Key Takeaways 💡

### Complete VPC Architecture Verification Checklist:

| Component | Configuration | Status |
|-----------|--------------|--------|
| ✅ VPC | 192.168.0.0/18 | Created |
| ✅ Subnet | 192.168.1.0/28 (Public) | Created |
| ✅ Internet Gateway | Attached to VPC | Created & Attached |
| ✅ Route Table | 0.0.0.0/0 → IGW | Configured |
| ✅ Subnet Association | Public subnet → Public route table | Complete |
| ✅ Network ACL | Inbound: Allow All (0.0.0.0/0) | Configured |
| ✅ Network ACL | Outbound: Allow All (0.0.0.0/0) | Configured |
| ✅ Security Group | Inbound: SSH, HTTP, HTTPS from 0.0.0.0/0 | Configured |
| ✅ Security Group | Outbound: All traffic | Configured |
| ✅ EC2 Instance | t3.micro in Public subnet | Launched |
| ✅ Public IP | Auto-assign enabled | Assigned |
| ✅ Internet Connectivity | ping google.com successful | Verified |

### VPC Building Best Practices:

| Do ✅ | Don't ❌ |
|------|---------|
| Follow left navigation pane in order | Skip steps or create components randomly |
| Name resources consistently (public route table, public subnet) | Use generic or confusing names |
| Associate route tables immediately after creation | Forget to associate route tables with subnets |
| Test with ping after each major change | Wait until the end to test connectivity |
| Document your IP allocations | Use overlapping CIDRs |
| Start with permissive rules, then restrict | Start with overly restrictive rules |

### Troubleshooting Flowchart:

```
Cannot ping internet?
        ↓
Check if instance has public IP
        ↓
Check route table for 0.0.0.0/0 → IGW
        ↓
Check subnet association with route table
        ↓
Check IGW is attached to VPC
        ↓
Check security group outbound rules
        ↓
Check NACL inbound/outbound rules
        ↓
Check OS-level firewall (if applicable)
```

---

## Important Notes ⚠️

### Critical Configuration Points:

1. **Route Table Association:** Every subnet MUST be associated with a route table. If not explicitly associated, it uses the main route table by default.

2. **IGW Route:** The destination 0.0.0.0/0 in a route table means "all IPv4 addresses" and targets traffic to the internet.

3. **NACL Rules:**
   - Rules are evaluated in order (lowest number first)
   - The *asterisk rule* is the default deny
   - NACLs are stateless - return traffic must be explicitly allowed

4. **Security Group Rules:**
   - Stateful - return traffic is automatically allowed
   - Can only have ALLOW rules (no DENY rules)
   - Changes take effect immediately

5. **Public IP Assignment:**
   - Can be auto-assigned at subnet level
   - Can be assigned manually via Elastic IP
   - Without a public IP, instance cannot be reached from internet

---

## Conclusion 🎉

I have now successfully:

- ✅ Investigated the customer's environment and identified configuration gaps
- ✅ Created a complete VPC with all necessary networking components
- ✅ Configured route tables, internet gateway, NACLs, and security groups
- ✅ Launched an EC2 instance in the public subnet
- ✅ Verified internet connectivity by successfully pinging google.com
- ✅ Documented the solution with clear explanations and best practices
- ✅ Provided a professional response to the customer

**Root Cause Summary:** The customer's VPC components were created but not properly configured to work together. Specifically, the route table lacked the internet gateway route, wasn't associated with the subnet, and security group/NACL rules needed proper configuration.

**Final Working Architecture:** The completed solution demonstrates a properly configured VPC with full internet connectivity, validated by successful ping responses from an EC2 instance to google.com.

---

## Additional Resources 📚

- [What is Amazon VPC?](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
- [IP Addressing in Your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-ip-addressing.html)
- [Route Tables for Your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)
- [Internet Gateways](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html)
- [Network ACLs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html)
- [Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)
- [Connecting to Your Linux Instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstances.html)
- [VPC CIDR Block Selection Guide](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-cidr-blocks.html)

---
