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

#Then Redeploy
Go to CloudFormation
Delete the failed stack

Wait for:

``
DELETE_COMPLETE
```
Created a new stack with the updated template

Expected Result
After fixing, your stack should show:

```
CREATE_COMPLETE
```











