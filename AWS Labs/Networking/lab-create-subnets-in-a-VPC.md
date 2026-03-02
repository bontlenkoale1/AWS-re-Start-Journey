# Create Subnets and Allocate IP addresses in an Amazon Virtual Private Cloud (Amazon VPC)
---

## Objectives 🎯
In this lab, I will:

✅ Summarize the customer scenario

✅ Create a Amazon Virtual Private Cloud (Amazon VPC) and understand how to create subnets and allocate IP addresses

✅ Familiarize yourself with the Amazon Web Services (AWS) Management Console

✅ Develop a solution to the customer's issue in this lab

✅ Summarize and describe my findings (group activity)

---
## What's This About?
Helping a customer (Paulo) set up their first VPC on AWS. They need ~15,000 IPs and a public subnet with at least 50 IPs.

## The Customer's Ask
"Hey, I'm new to AWS. Need help setting up a VPC. Want around 15,000 private IPs, using 192.x.x.x range (is that private? lol). Also need 50+ IPs in public subnet. Thanks!"

----

## Customer diagram


<img width="867" height="569" alt="vpc (2)" src="https://github.com/user-attachments/assets/03591ff2-9fd3-4289-b49a-7b1f52bb2fd4" />

Figure: In the customer's VPC architecture, the customer needs approximately 15,000 IP addresses for their Seattle office headquarters and 50 IP addresses for their operations department, which will be in the public subnet.


### Task 1️⃣: Figure Out the IP Math

First, checked what private ranges exist (RFC 1918):
- 10.0.0.0/8 (big)
- 172.16.0.0/12 (medium)
- **192.168.0.0/16 (perfect for Paulo)**

Used subnet calculator to find the right size:

| Need | What I Picked | Why |
|------|--------------|-----|
| 15,000 IPs | /18 (16,384 IPs) | Gives a little extra room |
| 50+ IPs in public | /26 (64 IPs) | AWS reserves 5, so 62 usable - plenty |

So went with: **192.168.0.0/18** for VPC and **192.168.1.0/26** for public subnet

### 1 Log Into AWS
- Clicked "Start Lab" (waited for it to be ready)
- Clicked "AWS" to open console
- Searched "VPC" in the search bar

### 2 Create the VPC
In VPC Dashboard:
- Clicked "Launch VPC Wizard"
- Picked "VPC with Single Public Subnet" (matches their diagram)
- Clicked "Select"

### 3 Fill in the Details

**VPC Settings:**
- IPv4 CIDR: 192.168.0.0/18 ← gives 16k IPs
- VPC Name: First VPC

 <img width="1913" height="918" alt="Screenshot 2026-02-22 164604" src="https://github.com/user-attachments/assets/a464779f-ee74-486d-9491-c13236c5211f" />


 
 **Public Subnet Settings:**
- CIDR: 192.168.1.0/26 ← gives 64 IPs
- Name: Public subnet
- AZ: No Preference


<img width="1919" height="918" alt="Screenshot 2026-02-22 164629" src="https://github.com/user-attachments/assets/c168cd14-9f5b-41be-8190-2195ab7202b4" />



Left everything else default.

### 4 Hit Create
Clicked "Create VPC" and waited for the success message.

### 5 Double-check It Worked
Went to "Your VPCs" in left menu. Saw "First VPC" listed with correct CIDR. ✅

----


# Task 2️⃣: Send the response to the customer 

"Good Day Paulo! Got your VPC set up. Here's what I did:

- **Picked 192.168.0.0/18** for your VPC - gives you 16k IPs (more than the 15k you wanted). And yep, 192.x.x.x is totally private - good memory!

- **Made your public subnet 192.168.1.0/26** - gives you 64 IPs total, 62 usable after AWS reserves a few. More than the 50 you needed.

- Everything's set up just like your diagram - VPC with internet gateway and that public subnet you wanted.


## Quick Reference

### Private IP Ranges (RFC 1918)
10.0.0.0 - 10.255.255.255 (10/8)
172.16.0.0 - 172.31.255.255 (172.16/12)
192.168.0.0 - 192.168.255.255 (192.168/16) ← used this



### What We Built
| Component | CIDR | IP Count | Good For |
|-----------|------|----------|----------|
| VPC | 192.168.0.0/18 | 16,384 | Seattle office (+room to grow) |
| Public Subnet | 192.168.1.0/26 | 64 | Operations dept |

## Helpful Links I Used
- [RFC 1918](https://datatracker.ietf.org/doc/html/rfc1918) - private IP ranges
- [Subnet Calculator](https://www.subnet-calculator.com/) - did the math for me
- [AWS VPC Docs](https://docs.aws.amazon.com/vpc/) - when I got stuck

## Things to Remember
- AWS grabs 5 IPs per subnet (network, router, DNS, etc.)
- Subnet must be inside VPC range (like Russian dolls - smaller one fits in bigger one)
- Test everything before calling it done

## Done!
Finished in about 45 mins. Customer's happy, VPC works, IP counts are right. Time for ☕

---

*Lab completed for Paulo's startup*

