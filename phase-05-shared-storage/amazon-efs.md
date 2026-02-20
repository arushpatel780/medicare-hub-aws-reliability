I created an Amazon EFS file system and connected it to the EC2 instances running in the Auto Scaling Group.

All EC2 instances:

Mount the same EFS file system

Read and write shared data

Access files consistently across AZs

🔹 Why Amazon EFS was chosen

Amazon EFS is designed for:

Shared file access

High availability

Automatic scaling

Multi-AZ durability

It is ideal for applications where:

Multiple servers need the same data

Servers are frequently replaced

Data must survive instance failures

🔹 How I did it (AWS Console)

Steps followed:
🧩 PART A: Create EFS File System
1️⃣ Go to EFS

AWS Console → Search EFS

Click Create file system

2️⃣ Basic Settings

Name → medicare-efs

VPC → medicare-vpc

Click Customize (don’t use quick create)

3️⃣ Network Access (IMPORTANT)

You will see mount targets per AZ.

For each Availability Zone:
| AZ         | Subnet            | Security Group  |
| ---------- | ----------------- | --------------- |
| us-east-1a | private-subnet-1a | medicare-ec2-sg |
| us-east-1b | private-subnet-1b | medicare-ec2-sg |
📌 This allows EC2 instances to mount EFS

4️⃣ File System Policy & Performance

Performance mode → General Purpose

Throughput → Bursting

Encryption → Enabled (default)

Click Create

⏳ Wait until Available

🧩 PART B: Allow NFS Traffic (CRITICAL)

EFS uses NFS (port 2049).

🔧 Update EC2 Security Group (medicare-ec2-sg)

Add inbound rule:
| Type | Port | Source          |
| ---- | ---- | --------------- |
| NFS  | 2049 | medicare-ec2-sg |


📌 This allows EC2 ↔ EFS communication

🧩 PART C: Mount EFS on EC2 (Auto Scaling Friendly)
5️⃣ Update Launch Template (NEW VERSION)

We must update user data so all new EC2 instances auto-mount EFS.

EC2 → Launch Templates

Select medicare-lt

Actions → Modify template

Create new version

6️⃣ Updated User Data (Paste This)

Replace old user data with this:
#!/bin/bash
yum update -y
yum install -y httpd amazon-efs-utils

systemctl start httpd
systemctl enable httpd

mkdir /efs
mount -t efs -o tls fs-XXXXXXXX:/ /efs

echo "<h1>MediCare Hub - Shared Storage via EFS</h1>" > /efs/index.html
ln -s /efs/index.html /var/www/html/index.html

⚠️ Replace fs-XXXXXXXX with your EFS File System ID
Click Create launch template version


7️⃣ Update Auto Scaling Group to New Version

EC2 → Auto Scaling Groups

Select medicare-asg

Edit → Launch template

Select Latest version

Save

📌 ASG will gradually replace instances.


🔁 How Reliability Works Here (Simple Explanation)

If an EC2 instance fails:

Auto Scaling launches a new EC2

New EC2 mounts the same EFS file system

Application data is immediately available

No data loss occurs

This removes instance-level storage dependency.

⚠️ Cost Awareness (Important Note)

For learning and documentation:

Amazon EFS was created temporarily

Screenshots were captured for proof

The file system was deleted immediately to control costs

This demonstrates:

Practical AWS usage

Cost awareness

Real-world decision making

✅ Phase 05 Outcome (Summary)

After completing Phase 05:

Application data is shared across EC2 instances

Storage survives EC2 termination

New instances work without manual setup

Reliability of the application is significantly improved

This phase ensures data durability at the compute layer.
