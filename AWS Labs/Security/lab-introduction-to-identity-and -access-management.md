# Introduction to AWS Identity and Access Management (IAM) 📝

## Lab Overview 🎯

In many business environments, access involves a single login to a computer or a network of computer systems that provides the user access to all resources on the network. This access includes rights to personal and shared folders on a network server, company intranets, printers, and other network resources and devices. Unauthorized users can quickly exploit these same resources if the access control and associated authentication procedures are not set up properly.

In this lab, I will explore users, user groups, and policies in the AWS Identity and Access Management (IAM) service.

---

## 🎯 Lab Objectives

After completing this lab, I will be able to:

- ✅ **Create and apply** an IAM password policy
- ✅ **Explore** pre-created IAM users and user groups
- ✅ **Inspect** IAM policies as applied to pre-created user groups
- ✅ **Add users** to user groups with specific capabilities
- ✅ **Locate and use** the IAM sign-in URL
- ✅ **Experiment** with the effects of policies on service access

---

## 🏗️ Lab Environment

The diagram below illustrates the current environment with the listed IAM users and groups:


![lab-scenario (1)](https://github.com/user-attachments/assets/5dd051eb-d288-4df5-b330-b695660ffc5e)

---

## 📚 What is IAM?

**AWS Identity and Access Management (IAM)** enables you to manage access to AWS services and resources securely. IAM can be used for the following:

| Feature | Description |
|---------|-------------|
| **Manage IAM users and their access** | Create users and assign individual security credentials (access keys, passwords, MFA devices). Manage permissions to control which operations a user can perform |
| **Manage IAM roles and their permissions** | An IAM role is similar to a user but is intended to be assumable by anyone who needs it, rather than being uniquely associated with one person |
| **Manage federated users and their permissions** | Activate identity federation to allow existing enterprise users to access AWS without creating an IAM user for each identity |

---

## 📋 IAM Policy Structure

An IAM policy defines what actions are allowed or denied for specific AWS resources. The basic structure of a policy statement is:

```json
{
  "Effect": "Allow" or "Deny",
  "Action": "service:APIcall" (e.g., "ec2:DescribeInstances"),
  "Resource": "ARN of resource" (e.g., "*" for any resource)
}
```

- **Effect**: Indicates whether to `Allow` or `Deny` the permissions
- **Action**: Specifies the API calls that can be made against an AWS service
- **Resource**: Defines the scope of entities covered by the policy rule

---

## 🔧 Step-by-Step Lab Implementation

### **Task 1️⃣: Create an Account Password Policy**

In this task, I created a custom password policy for my AWS account. This policy affects all users associated with the account.

#### Steps:

1. **Navigate to IAM**
   - In the AWS Management Console, search for and select **IAM**
   - Note my current Region (e.g., Oregon) in the upper-right corner

2. **Access Account Settings**
   - In the left navigation pane, choose **Account settings**
   - Review the default password policy currently in effect

3. **Configure Custom Password Policy**
   - Choose **Change password policy**
   - Configure the following options:
     - **Enforce minimum password length**: Change from `8` to `10` characters
     - **Require at least one uppercase letter**: ✅ Select
     - **Require at least one lowercase letter**: ✅ Select
     - **Require at least one number**: ✅ Select
     - **Require at least one non-alphanumeric character**: ✅ Select
     - **Enable password expiration**: ✅ Select (default: `90` days)
     - **Prevent password reuse**: ✅ Select (default: `5` passwords)
     - **Password expiration requires administrator reset**: ❌ Leave unchecked
   - Choose **Save changes**

<img width="1908" height="915" alt="Screenshot 2026-02-25 185414" src="https://github.com/user-attachments/assets/75d5a82a-1caa-464c-bb4c-097eab69084e" />

4. **Verify Implementation**
   - These changes take effect at the AWS account level
   - Apply to every user associated with the account

#### ✅ Task 1 Summary
In this task, I strengthened password requirements by creating a custom password policy. The various password options selected make passwords that users create much more difficult to crack.

---

### **Task 2: Explore Users and User Groups**

In this task, I explore pre-created users and user groups in IAM.

#### Pre-created IAM Users:

| Username | Initial Status |
|----------|----------------|
| user-1 | No permissions, no group membership |
| user-2 | No permissions, no group membership |
| user-3 | No permissions, no group membership |

#### Steps:

1. **Explore Users**
   - In the left navigation pane, choose **Users**
   - Select **user-1** to view the Summary page
   - Review the tabs:
     - **Permissions tab**: Shows user-1 has no permissions
     - **Groups tab**: Shows user-1 is not a member of any groups
     - **Security credentials tab**: Shows user-1 has a console password assigned

2. **Explore User Groups**
   - In the left navigation pane, choose **User groups**
   - The following groups have been pre-created:

| Group Name | Attached Policy | Policy Type | Permissions |
|------------|-----------------|-------------|-------------|
| **EC2-Support** | `AmazonEC2ReadOnlyAccess` | AWS Managed | List/describe EC2, ELB, CloudWatch, Auto Scaling |
| **S3-Support** | `AmazonS3ReadOnlyAccess` | AWS Managed | Get/list S3 resources |
| **EC2-Admin** | `EC2-Admin-Policy` | Customer Inline | View, start, and stop EC2 instances |

3. **Inspect EC2-Support Group**
   - Choose **EC2-Support** group
   - Select the **Permissions** tab
   - Next to `AmazonEC2ReadOnlyAccess`, click the **+** to expand the policy
   - Observe the permissions that grant read-only access to EC2 resources

4. **Inspect S3-Support Group**
   - Navigate back to **User groups**
   - Choose **S3-Support** group
   - Select the **Permissions** tab
   - Expand `AmazonS3ReadOnlyAccess` to view S3-specific permissions

5. **Inspect EC2-Admin Group**
   - Navigate back to **User groups**
   - Choose **EC2-Admin** group
   - Select the **Permissions** tab
   - Expand `EC2-Admin-Policy` (Customer inline policy)
   - Observe permissions for viewing, starting, and stopping EC2 instances

#### ✅ Task 2 Summary
In this task, I viewed pre-created users and user groups and learned about attached policies and the differences between group permissions.

<img width="1900" height="914" alt="Screenshot 2026-02-25 185917" src="https://github.com/user-attachments/assets/b89fc471-b8f4-4870-b84f-774c534c6f4b" />


---

### **Task 3: Add Users to User Groups**

#### Business Scenario

My company is growing its AWS usage with many EC2 instances and significant S3 storage. I need to grant access to new staff based on their job functions:

| User | Group Assignment | Permissions Needed |
|------|------------------|-------------------|
| **user-1** | S3-Support | Read-only access to Amazon S3 |
| **user-2** | EC2-Support | Read-only access to Amazon EC2 |
| **user-3** | EC2-Admin | View, start, and stop EC2 instances |

#### Steps:

1. **Add user-1 to S3-Support Group**
   - In the left navigation pane, choose **User groups**
   - Select **S3-Support** group
   - Choose the **Users** tab
   - Select **Add users**
   - Check the box for **user-1**
   - Choose **Add users**
   - Verify user-1 now appears in the Users tab

<img width="1914" height="918" alt="Screenshot 2026-02-25 190254" src="https://github.com/user-attachments/assets/144dc723-1161-4981-ad31-5229eddecc3e" />


2. **Add user-2 to EC2-Support Group**
   - Navigate to **User groups**
   - Select **EC2-Support** group
   - Choose the **Users** tab
   - Select **Add users**
   - Check the box for **user-2**
   - Choose **Add users**
   - Verify user-2 now appears in the Users tab
  
<img width="1918" height="914" alt="Screenshot 2026-02-25 190355" src="https://github.com/user-attachments/assets/6e36bef0-e5f8-45b3-8aa6-dca60603037a" />


3. **Add user-3 to EC2-Admin Group**
   - Navigate to **User groups**
   - Select **EC2-Admin** group
   - Choose the **Users** tab
   - Select **Add users**
   - Check the box for **user-3**
   - Choose **Add users**
   - Verify user-3 now appears in the Users tab

<img width="1913" height="916" alt="Screenshot 2026-02-25 190452" src="https://github.com/user-attachments/assets/1ac17a72-6c9f-4867-b22a-c94442ceea00" />


4. **Verify Group Membership**
   - Navigate back to **User groups**
   - Each group should show a **1** in the Users column
   - If not, revisit steps to confirm assignments

<img width="1912" height="917" alt="Screenshot 2026-02-25 190530" src="https://github.com/user-attachments/assets/4654d008-1473-46d8-bd42-47931680d626" />

#### ✅ Task 3 Summary
In this task, I added all associated users to their respective user groups based on job function requirements.

---

### **Task 4: Sign In and Test User Permissions**

In this task, I test the permissions of each IAM user.

#### Step 1: Obtain IAM Sign-in URL

1. In the left navigation pane, choose **Dashboard**
2. Locate the **Sign-in URL for IAM users** in the AWS Account section
   - Format: `https://123456789012.signin.aws.amazon.com/console`
3. Copy this URL to a text editor

#### Step 2: Test user-1 (S3 Support)

1. **Open a private/incognito window:**
   - **Firefox**: Menu → New Private Window
   - **Chrome**: Ellipsis → New Incognito window
   - **Edge**: Ellipsis → New InPrivate window

2. **Sign in as user-1:**
   - Paste the Sign-in URL and press Enter
   - **Username**: `user-1`
   - **Password**: `Lab-Password1`
   - Choose **Sign in**

<img width="1919" height="1021" alt="Screenshot 2026-02-25 191038" src="https://github.com/user-attachments/assets/1039e722-3ddb-4093-a4be-52552e93119e" />

3. **Test S3 Access:**
   - From Services menu, choose **S3**
   - Select a bucket and browse contents
   - ✅ **Expected**: Can view S3 buckets and contents

4. **Test EC2 Access:**
   - From Services menu, choose **EC2**
   - In left navigation, choose **Instances**
   - ❌ **Expected**: Error message: *"You are not authorized to perform this operation"*

<img width="1908" height="912" alt="Screenshot 2026-02-25 191344" src="https://github.com/user-attachments/assets/9e2c6c72-895b-4d24-98c8-1538a9c32ee5" />


5. **Sign out user-1:**
   - At top of screen, choose **user-1** → **Sign out**

#### Step 3: Test user-2 (EC2 Support)

1. **Sign in as user-2:**
   - Paste Sign-in URL in private window
   - **Username**: `user-2`
   - **Password**: `Lab-Password2`
   - Choose **Sign in**

2. **Test EC2 Read Access:**
   - From Services menu, choose **EC2**
   - In left navigation, choose **Instances**
   - Verify Region matches your lab Region (e.g., Oregon)
   - ✅ **Expected**: Can view EC2 instance

<img width="1913" height="908" alt="Screenshot 2026-02-25 192501" src="https://github.com/user-attachments/assets/64b76c8e-e3d0-46f6-b26b-c495488f28f1" />

3. **Test EC2 Modify Permissions:**
   - Select the EC2 instance
   - From **Instance state** dropdown, choose **Stop instance**
   - In confirmation, choose **Stop**
   - ❌ **Expected**: Error: *"Failed to stop the instance. You are not authorized to perform this operation"*
   - Choose **Cancel**

<img width="1914" height="911" alt="Screenshot 2026-02-25 191818" src="https://github.com/user-attachments/assets/8ae1c9c2-6e73-4e62-832e-b47423d840c4" />

4. **Test S3 Access:**
   - From Services menu, choose **S3**
   - ❌ **Expected**: *"You don't have permissions to list buckets"*

5. **Sign out user-2:**
   - At top of screen, choose **user-2** → **Sign out**

#### Step 4: Test user-3 (EC2 Admin)

1. **Sign in as user-3:**
   - Paste Sign-in URL in private window
   - **Username**: `user-3`
   - **Password**: `Lab-Password3`
   - Choose **Sign in**

2. **Test EC2 Admin Permissions:**
   - From Services menu, choose **EC2**
   - In left navigation, choose **Instances**
   - Select the EC2 instance
   - From **Instance state** dropdown, choose **Stop instance**
   - In confirmation, choose **Stop**
   - ✅ **Expected**: Instance enters *Stopping* state and shuts down

3. **Close the private window**

#### ✅ Task 4 Summary

| User | Group | Expected S3 Access | Expected EC2 Access | Actual Result |
|------|-------|-------------------|---------------------|---------------|
| user-1 | S3-Support | ✅ Read-only | ❌ No access | ✅ Verified |
| user-2 | EC2-Support | ❌ No access | ✅ Read-only | ✅ Verified |
| user-3 | EC2-Admin | ❌ No access | ✅ Start/Stop | ✅ Verified |

---

## 🎓 Conclusion

Congratulations!
I have successfully completed this lab and demonstrated proficiency in:

| Objective | Completed |
|-----------|-----------|
| Creating and applying an IAM password policy | ✅ |
| Exploring pre-created IAM users and user groups | ✅ |
| Inspecting IAM policies as applied to user groups | ✅ |
| Adding users to groups with specific capabilities | ✅ |
| Locating and using the IAM sign-in URL | ✅ |
| Testing policy effects on service access | ✅ |

---

## 📝 Key Takeaways

- **IAM Password Policies** enforce security requirements across all users
- **User Groups** simplify permission management by organizing users with common access needs
- **Managed Policies** are pre-built and can be attached to multiple users/groups
- **Inline Policies** are specific to a single user or group
- **Least Privilege Access** ensures users have only the permissions needed for their role
- **Testing** different user accounts validates policy effectiveness

---

## 🔗 Additional Resources

- [AWS IAM Documentation](https://docs.aws.amazon.com/iam/)
- [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [IAM Policy Examples](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_examples.html)

---
