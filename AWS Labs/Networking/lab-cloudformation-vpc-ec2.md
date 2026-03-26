#  AWS CloudFormation Lab – VPC & EC2 Deployment

##  Overview
This project demonstrates how to use **AWS CloudFormation** to provision cloud infrastructure automatically. The goal was to create a fully functional environment consisting of a Virtual Private Cloud (VPC), networking components, and an EC2 instance inside a private subnet.

This lab was completed as part of the **AWS re/Start program**, focusing on Infrastructure as Code (IaC) principles.

---

## Architecture Components

The CloudFormation template provisions the following resources:

- **Amazon VPC**
  - CIDR block: `10.0.0.0/16`

- **Internet Gateway**
  - Attached to the VPC to enable internet connectivity

- **Private Subnet**
  - CIDR block: `10.0.1.0/24`

- **Route Table**
  - Configured with a route to the Internet Gateway (`0.0.0.0/0`)
  - Associated with the subnet

- **Security Group**
  - Allows SSH access (port 22) from anywhere (`0.0.0.0/0`)

- **Amazon EC2 Instance**
  - Instance type: `t3.micro`
  - Deployed inside the private subnet

---

##  Deployment Steps

1. Open the AWS Management Console
2. Navigate to **CloudFormation**
3. Click **Create Stack**
4. Choose **With new resources (standard)**
5. Upload or paste the CloudFormation template
6. Click **Next** and keep default settings
7. Click **Create Stack**
8. Wait for the status:
CREATE_COMPLETE
I encounted an error, Invalid AMI ID


---

##  Challenges & Solutions

###  Issue: Invalid AMI ID
- Error:
The image id does not exist

- **Cause:** AMIs are region-specific
- **Solution:** Fixed the ami ImageId by going to EC2 launch instance and copied the ImageId and replaced it in my yaml.
```
MyEC2Instance:
  Type: AWS::EC2::Instance
  Properties:
    InstanceType: t3.micro
    SubnetId: !Ref MySubnet
    SecurityGroupIds:
      - !Ref MySecurityGroup
    ImageId: ami-03caad32a158f72db
    Tags:
      - Key: Name
        Value: PrivateEC2
```

```yaml
ImageId: ami-03caad32a158f72db
```

# Then Redeploy
Go to CloudFormation
Delete the failed stack

Wait for:

```
DELETE_COMPLETE
```
Created a new stack with the updated template

Expected Result
After fixing, your stack should show:

```
CREATE_COMPLETE
```


<img width="1910" height="915" alt="Screenshot 2026-03-26 120922" src="https://github.com/user-attachments/assets/9d8805fd-e45f-48f4-b11d-5f8fdfb61f45" />
<img width="1910" height="909" alt="Screenshot 2026-03-26 120950" src="https://github.com/user-attachments/assets/62d44e6e-6c89-441a-b71e-c9c629aa0711" />


<img width="1908" height="908" alt="Screenshot 2026-03-26 121034" src="https://github.com/user-attachments/assets/f1a88e88-9060-4372-a9b4-f8730f8b4799" />
<img width="1905" height="901" alt="Screenshot 2026-03-26 121004" src="https://github.com/user-attachments/assets/5c7f6575-769e-436d-9c91-6a357f38930c" />
<img width="1910" height="909" alt="Screenshot 2026-03-26 120950" src="https://github.com/user-attachments/assets/10584508-f60e-4fd7-8531-dc2aaf658778" />
<img width="1910" height="906" alt="Screenshot 2026-03-26 121337" src="https://github.com/user-attachments/assets/de13c2d0-c056-4d3e-9c9c-fcdea0d0e506" />

# Key Learnings
• Infrastructure as Code (IaC) using CloudFormation

•VPC networking fundamentals (subnets, route tables, gateways)

•Region-specific configurations in AWS

•Debugging CloudFormation stack errors

•Automating cloud resource provisioning

# Concepts Used
AWS CloudFormation ✅

Amazon VPC✅

EC2 Instances ✅

Security Groups✅

Internet Gateway✅

Route Tables & Subnet Associations ✅

# Project Outcome
Successfully deployed all resources✅

Stack reached CREATE_COMPLETE status✅

EC2 instance launched within the private subnet ✅

#Final Architecture

![q7_xH_nFr82AOgK_8JSvzInmCrzLrIxOz_Co30SAChaSZ3DjzV5x6vIB9i4OG148YWWOX_WjgIrLaHNiIanOM4_MeL-Ti9EtWmwRTo51QnCpjP6cJEKNDHDCFgY6qFHVrciLedTsxYT-DiATM_am8Wq-zK67-qnV7zDDFrT14uA_tL3GXwCmnUig9X2pcVgW](https://github.com/user-attachments/assets/c1093c46-deeb-42e1-a7e1-aea36647bc02)





