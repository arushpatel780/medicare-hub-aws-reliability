I created an Auto Scaling Group (ASG) using the launch template.

The ASG ensures:

A fixed minimum number of EC2 instances is always running

New instances are launched automatically if one fails

🔹 Why Auto Scaling is needed

Auto Scaling solves multiple reliability problems:

If an EC2 instance crashes → new one launches automatically

If traffic increases → system can scale out

If traffic decreases → system scales in (cost control)

This creates a self-healing system, which is a key reliability principle.

🔹 How I did it (AWS Console)

Steps:
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


Multi-AZ Deployment (Very Important)

The Auto Scaling Group was configured to:

Launch instances in multiple Availability Zones

Avoid placing all servers in a single AZ

This means:

If one AZ fails, the application still runs in another AZ

No single infrastructure failure can stop the app
After completing Phase 02:

The application runs on multiple EC2 instances

Instances are automatically replaced on failure

Compute layer is fault-tolerant and scalable

Manual server management is eliminated

This phase makes the system self-healing, which is essential for reliable applications.
