# 📊 Lab: Monitor an EC2 Instance

## Lab Overview

Logging and monitoring are essential techniques that work together to ensure system performance baselines and security guidelines are consistently met.

**Logging** refers to recording and storing data events as log files. Logs contain low-level details that provide visibility into how applications or systems perform under specific circumstances. From a security standpoint, logging helps security administrators identify red flags that might otherwise be overlooked.

**Monitoring** is the process of analyzing and collecting data to help ensure optimal performance. Monitoring helps detect unauthorized access and aligns service usage with organizational security policies.

In this lab, I created an Amazon CloudWatch alarm that triggers when an EC2 instance exceeds a specific CPU utilization threshold. I configured an Amazon Simple Notification Service (SNS) subscription that sends an email alert when the alarm activates. I then logged into the EC2 instance and ran a stress test to simulate a malicious actor gaining control and spiking the CPU—a scenario that could indicate malware or unauthorized activity.

---

## 🎯 Lab Objectives

After completing this lab, I successfully:

- ✅ **Created** an Amazon SNS notification topic and subscription
- ✅ **Configured** a CloudWatch alarm for CPU utilization monitoring
- ✅ **Stress tested** an EC2 instance to simulate malicious activity
- ✅ **Confirmed** that an Amazon SNS email alert was sent
- ✅ **Created** a CloudWatch dashboard for visualization

---

## 📋 Prerequisites

The lab environment came pre-configured with:
- **Stress Test EC2 instance** with an attached IAM role for Systems Manager access
- All backend components (EC2, IAM roles, and supporting AWS services) pre-built

---

## 🔧 Step-by-Step Implementation

### **Task 1️⃣: Configure Amazon SNS Notification**

In this task, I created an SNS topic and subscribed to it with my email address. This will be the notification channel for CloudWatch alarms.

#### Steps:

1. **Navigate to Amazon SNS**
   - In the AWS Management Console, I searched for and selected **Simple Notification Service (SNS)**

2. **Create an SNS Topic**
   - In the left navigation, I expanded the menu and chose **Topics**
   - Selected **Create topic**
   - Configured the following options:
     - **Type**: `Standard` ✓
     - **Name**: `MyCwAlarm`
   - Chose **Create topic**
<img width="1900" height="912" alt="Screenshot 2026-03-03 080753" src="https://github.com/user-attachments/assets/fa68713e-53ce-47c2-80b3-35d5c380ab45" />

3. **Create a Subscription**
   - On the `MyCwAlarm` details page, I selected the **Subscriptions** tab
   - Chose **Create subscription**
   - Configured the following options:
     - **Topic ARN**: (default, pre-populated)
     - **Protocol**: `Email` (from dropdown)
     - **Endpoint**: `[my-email-address]` (I entered a valid email I can access)
   - Chose **Create subscription**

<img width="1906" height="910" alt="Screenshot 2026-03-03 081020" src="https://github.com/user-attachments/assets/00387b8c-32d8-4758-b744-ac1b5048f42f" />

4. **Confirm Subscription**
   - The subscription status initially showed **Pending confirmation**
  
<img width="1890" height="819" alt="Screenshot 2026-03-03 081112" src="https://github.com/user-attachments/assets/51c01377-5d23-491a-8c48-4471401baa78" />
   
   - I checked my email inbox and found an **AWS Notification - Subscription Confirmation** message
     
     <img width="1913" height="925" alt="Screenshot 2026-03-03 081238" src="https://github.com/user-attachments/assets/3f6f2a98-950e-4ff0-a29d-ff550ad1c65a" />

   - Clicked **Confirm subscription** in the email
   - Returned to the AWS Console and navigated to **Subscriptions**
   - Verified the status had changed to **Confirmed** ✓


<img width="1904" height="909" alt="Screenshot 2026-03-03 081302" src="https://github.com/user-attachments/assets/16c3899e-4535-4e59-be8c-52d6380acda4" />

#### ✅ Task 1 Summary
I successfully created an SNS topic and configured an email subscription. This topic is now ready to send alerts to my email address when triggered by CloudWatch alarms.
<img width="1912" height="907" alt="Screenshot 2026-03-03 081331" src="https://github.com/user-attachments/assets/e8c6a48e-438b-4b1a-b299-fc829812d24a" />

---

### **Task 2️⃣: Create a CloudWatch Alarm**

In this task, I explored CloudWatch metrics and created an alarm that will trigger when the Stress Test EC2 instance exceeds 60% CPU utilization.

#### Steps:

1. **Navigate to CloudWatch**
   - In the AWS Management Console, I searched for and selected **CloudWatch**

2. **Explore CloudWatch Metrics**
   - In the left navigation, I expanded the **Metrics** dropdown and chose **All metrics**
   - Selected **EC2** → **Per-Instance Metrics**
   - Located the Stress Test EC2 instance and selected the checkbox for **CPUUtilization**
   - Observed the graph showing CPU utilization (approximately 0% at baseline)
<img width="1904" height="906" alt="Screenshot 2026-03-03 081914" src="https://github.com/user-attachments/assets/8127760c-9a6c-4342-9ac3-49d45c2c6565" />

3. **Create the Alarm**
   - In the left navigation, I expanded the **Alarms** dropdown and chose **All alarms**
   - Selected **Create alarm**
   - Chose **Select metric**
   - Navigated to **EC2** → **Per-Instance Metrics**
   - Selected the checkbox for **CPUUtilization** for the Stress Test instance
   - Chose **Select metric**

4. **Configure Metric and Conditions**
   - **Metric**:
     - **Metric name**: `CPUUtilization` (pre-populated)
     - **InstanceId**: (default)
     - **Statistic**: `Average`
     - **Period**: `1 minute` (from dropdown)
   - **Conditions**:
     - **Threshold type**: `Static` ✓
     - **Whenever CPUUtilization is...**: `Greater > threshold`
     - **than... Define the threshold value**: `60`
   - Chose **Next**
<img width="1915" height="916" alt="Screenshot 2026-03-03 082339" src="https://github.com/user-attachments/assets/30b834b8-8585-4c51-b629-f7efa74294a6" />
<img width="1904" height="907" alt="Screenshot 2026-03-03 082436" src="https://github.com/user-attachments/assets/11571726-6371-4361-a334-e426b9d6929d" />

5. **Configure Actions**
   - **Notification**:
     - **Alarm state trigger**: `In alarm` ✓
     - **Select an SNS topic**: `Select an existing SNS topic`
     - **Send a notification to...**: Selected `MyCwAlarm` from dropdown
   - Chose **Next**
<img width="1918" height="906" alt="Screenshot 2026-03-03 082643" src="https://github.com/user-attachments/assets/a8acd02e-5f7d-4f77-8208-7dc89a593bd5" />

6. **Add Name and Description**
   - **Alarm name**: `LabCPUUtilizationAlarm`
   - **Alarm description**: `CloudWatch alarm for Stress Test EC2 instance CPUUtilization`
   - Chose **Next**

<img width="1914" height="908" alt="Screenshot 2026-03-03 082749" src="https://github.com/user-attachments/assets/b773b728-27dd-4f68-a89a-05a4e788a3e6" />

7. **Review and Create**
   - Reviewed the configuration on the Preview and create page
   - Chose **Create alarm**

#### ✅ Task 2 Summary
I successfully created a CloudWatch alarm that will enter the **In alarm** state when CPU utilization exceeds 60%. When triggered, it will send a notification to my SNS topic.

---

### **Task 3️⃣: Test the CloudWatch Alarm**

In this task, I simulated malicious activity by stress-testing the EC2 instance to spike CPU utilization to 100%, triggering the alarm and email notification.

#### Steps:

1. **Access the Stress Test Instance**
   - Returned to the Vocareum console page
   - Clicked the **AWS Details** button
   - Located the `EC2InstanceURL` link and opened it in a new browser tab
   - This connected me directly to the Stress Test EC2 instance via Systems Manager Session Manager

2. **Run CPU Stress Test**
   - In the terminal, I ran the following command to simulate high CPU load:
     ```bash
     sudo stress --cpu 10 -v --timeout 400s
     ```
   - This command:
     - Runs for **400 seconds**
     - Loads the CPU to **100%**
     - Automatically decreases CPU to 0% after the allotted time

<img width="1915" height="917" alt="Screenshot 2026-03-03 084136" src="https://github.com/user-attachments/assets/2684abd7-cd7d-448f-843b-bcb010a34460" />

3. **Monitor CPU in Real-Time**
   - Opened a second terminal session using the same `EC2InstanceURL`
   - Ran the following command to view live CPU usage:
     ```bash
     top
     ```
   - Observed CPU utilization spike to near 100%

4. **Monitor CloudWatch Alarm**
   - Returned to the AWS Console with CloudWatch Alarms open
   - Selected **LabCPUUtilizationAlarm**
   - Refreshed the page every minute to monitor status
   - Watched the graph as CPUUtilization climbed above the 60% threshold
   - After a few minutes, the alarm status changed to **In alarm** ✓

<img width="1908" height="907" alt="Screenshot 2026-03-03 083242" src="https://github.com/user-attachments/assets/365975b6-bf7d-43be-90c0-ac00c6524d22" />

5. **Verify Email Notification**
   - Checked my email inbox for the address used in the SNS subscription
   - Found a new email notification from **AWS Notifications**
   - Email confirmed the alarm had been triggered ✓
<img width="1913" height="824" alt="Screenshot 2026-03-03 083337" src="https://github.com/user-attachments/assets/0219a5e5-1dc5-45a5-a30d-e434438e81cd" />

#### ✅ Task 3 Summary
I successfully simulated malicious activity by stress-testing the EC2 instance to 100% CPU utilization. This triggered the CloudWatch alarm, which changed to **In alarm** state and sent an email notification through SNS—exactly the behavior I wanted to achieve.

---

### **Task 4️⃣: Create a CloudWatch Dashboard**

In this task, I created a customizable dashboard to monitor CPU utilization metrics in a single view.

#### Steps:

1. **Navigate to CloudWatch Dashboards**
   - In the CloudWatch console, I selected **Dashboards** from the left navigation
   - Chose **Create dashboard**

2. **Configure Dashboard**
   - **Dashboard name**: `LabEC2Dashboard`
   - Chose **Create dashboard**

3. **Add Widget**
   - Selected **Line** as the widget type
   - Chose **Metrics** as the data source
   - Navigated to **EC2** → **Per-Instance Metrics**
   - Selected the checkbox for:
     - **Instance name**: `Stress Test`
     - **Metric name**: `CPUUtilization`
   - Chose **Create widget**
<img width="1906" height="910" alt="Screenshot 2026-03-03 083845" src="https://github.com/user-attachments/assets/cae0e6f3-89fc-4234-b40f-662c25bedafc" />

4. **Save Dashboard**
   - Reviewed the widget displaying CPU utilization metrics
   - Chose **Save dashboard**

#### ✅ Task 4 Summary
I created a CloudWatch dashboard providing quick, visual access to CPU utilization metrics for the Stress Test instance. This dashboard will allow me to monitor future performance anomalies efficiently.

---

## 📊 Before and After Comparison

| Test Scenario | Before Monitoring | After Monitoring | Result |
|------|-------------------|-------------------|--------|
| CPU spike detection | ❌ No visibility | ✅ CloudWatch alarm triggers | ✅ Success |
| Alert notification | ❌ No alerting | ✅ SNS email sent | ✅ Success |
| Performance visualization | ❌ No dashboard | ✅ Custom dashboard created | ✅ Success |
| Incident response time | ❌ Manual/Unknown | ✅ Immediate email alert | ✅ Improved |

---

## 🎓 Lab Summary

In this lab, I successfully implemented a complete monitoring and alerting solution:

1. **Created an SNS notification system** to deliver alerts via email
2. **Configured a CloudWatch alarm** to monitor CPU utilization and trigger at 60% threshold
3. **Simulated malicious activity** by stress-testing an EC2 instance to 100% CPU
4. **Verified the alert chain** worked—alarm triggered and email was sent
5. **Built a CloudWatch dashboard** for ongoing visualization and monitoring

This scenario simulates a real-world security concern: a malicious actor gaining control of an EC2 instance and spiking CPU utilization (which could indicate malware, crypto mining, or other unauthorized activity). The monitoring solution I implemented provides early warning of such incidents.

---

## 🎯 Objectives Achieved

| Objective | Completed |
|-----------|-----------|
| Create an Amazon SNS notification topic and subscription | ✅ |
| Configure a CloudWatch alarm with threshold-based triggering | ✅ |
| Stress test an EC2 instance to simulate malicious activity | ✅ |
| Confirm Amazon SNS email delivery upon alarm activation | ✅ |
| Create a CloudWatch dashboard for metrics visualization | ✅ |

---

## 📝 Key Takeaways

- **CloudWatch** provides comprehensive monitoring and observability for AWS resources
- **SNS** enables real-time notifications across multiple channels (email, SMS, etc.)
- **Alarms** can be configured to trigger on specific thresholds, enabling automated responses
- **Stress testing** validates that monitoring systems work as expected
- **Dashboards** provide at-a-glance visibility into system health and performance
- **Early detection** of anomalies (like CPU spikes) is critical for security incident response

---

## 🔗 Additional Resources

- [Amazon CloudWatch Documentation](https://docs.aws.amazon.com/cloudwatch/)
- [Amazon SNS Documentation](https://docs.aws.amazon.com/sns/)
- [CloudWatch Alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html)
- [EC2 Monitoring Best Practices](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring_ec2.html)

---

*This lab is part of the AWS re/Start program curriculum and was completed as part of my cloud monitoring and security training.*
