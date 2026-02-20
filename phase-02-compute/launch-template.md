I created an EC2 Launch Template that defines how new EC2 instances should be created automatically.

The launch template includes:

Operating system

Instance type

Security configuration

Startup script (user data)

🔹 Why a launch template is needed

A launch template ensures:

Every EC2 instance is created consistently

Auto Scaling can quickly launch new instances

No manual configuration is required during failures

Without a launch template:

Recovery would be slow

Configuration errors could occur

Reliability would decrease

🔹 How I did it (AWS Console)

Steps followed:

Opened EC2 Dashboard

Navigated to Launch Templates

Created a new template named medicare-lt

Selected Amazon Linux 2 AMI

Chose t2.micro / t3.micro (Free Tier eligible)

Attached EC2 security group

Added user data script to install Apache

🔹 User Data (What happens when EC2 starts)

When a new EC2 instance launches, this script:

Installs Apache web server

Starts the service automatically

Displays a simple web page

This proves the instance is:

Working correctly

Ready to receive traffic

1️⃣ Go to Launch Templates

AWS Console → Search EC2

Left menu → Launch Templates

Click Create launch template

2️⃣ Launch Template Details

Fill only what is needed (don’t overconfigure).

Launch template name → medicare-lt

Template version description → Initial version

❌ Do NOT check “Provide guidance”

3️⃣ AMI (Amazon Machine Image)

Click Browse AMIs

Choose:
✅ Amazon Linux 2 AMI (Free Tier Eligible)

📌 Why?

Stable

Free Tier supported

Common in interviews

4️⃣ Instance Type (VERY IMPORTANT)

Select → t2.micro
(or t3.micro if t2 not available)

📌 Free Tier safe
📌 Good enough for demo apps

5️⃣ Key Pair (Optional but Recommended)

Select your existing key pair
OR

Create a new one (RSA)

📌 Needed if you want SSH access later

6️⃣ Network Settings

Leave defaults here ❗
(ASG will decide subnets later)

7️⃣ Security Group

Click Create new security group

Name → medicare-ec2-sg

Description → Allow HTTP from ALB

| Type | Port | Source    |
| ---- | ---- | --------- |
| HTTP | 80   | 0.0.0.0/0 |
| SSH  | 22   | My IP     |

📌 SSH only for admin
📌 HTTP for app traffic
8️⃣ User Data (IMPORTANT)

Scroll down → Advanced details → User data


#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd

echo "<h1>MediCare Hub - Reliable EC2 Instance</h1>" > /var/www/html/index.html

📌 This:

Installs Apache

Starts web server automatically

Proves instance health to ALB

9️⃣ Create Launch Template

Scroll down → Click Create launch template

✅ Launch Template is ready

📸 Screenshot for GitHub:

Launch template summary

User data section

🧩 PART B: Create Auto Scaling Group (ASG)

🎯 Purpose:
Auto Scaling ensures:

If EC2 fails → new EC2 launches

If load increases → scale out

If load decreases → scale in

🔟 Create Auto Scaling Group

EC2 → Auto Scaling Groups

Click Create Auto Scaling group

1️⃣1️⃣ ASG Basics

Auto Scaling group name → medicare-asg

Launch template → medicare-lt

Version → Latest

Click Next

1️⃣2️⃣ Choose VPC & Subnets

VPC → medicare-vpc

Subnets →
✅ private-subnet-1a
✅ private-subnet-1b

📌 THIS IS KEY
➡️ Instances are spread across multiple AZs

1️⃣3️⃣ Load Balancer (We’ll attach ALB properly next)

For now:

Select Attach to an existing load balancer

Choose Target Group (if already created)

OR select Skip (OK for now)

📌 We’ll attach ALB cleanly in next phase

Click Next

1️⃣4️⃣ Set Capacity (IMPORTANT)

Set exactly this:

Minimum capacity → 2

Desired capacity → 2

Maximum capacity → 4

📌 Reliability logic:

App survives 1 instance failure

Can scale under traffic

1️⃣5️⃣ Scaling Policy

Choose:

Target tracking scaling

Metric → Average CPU Utilization

Target → 50%

📌 Simple, safe, realistic

1️⃣6️⃣ Skip Notifications & Tags (Optional)

You can skip notifications

Tags (optional):

Key: Project

Value: MediCare-Hub

1️⃣7️⃣ Create Auto Scaling Group

Click Create Auto Scaling group

🎉 DONE
