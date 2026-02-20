I created an Application Load Balancer (ALB) to distribute incoming traffic across multiple EC2 instances.

The ALB acts as:

The public entry point for users

A traffic manager

A health monitoring system

🔹 Why Application Load Balancer was chosen

An Application Load Balancer is ideal because:

It works at the HTTP level

Supports health checks

Integrates directly with Auto Scaling

Can handle large traffic volumes reliably

This makes it suitable for web-based medical applications.



steps:

4️⃣ Go to Load Balancers

EC2 → Load Balancers

Click Create load balancer

5️⃣ Select Load Balancer Type

Choose:
✅ Application Load Balancer

Click Create

6️⃣ Basic Configuration

Load balancer name → medicare-alb

Scheme → Internet-facing

IP address type → IPv4

7️⃣ Network Mapping

VPC → medicare-vpc

Mappings:

us-east-1a → public-subnet-1a

us-east-1b → public-subnet-1b

📌 ALB must be in public subnets

8️⃣ Security Group for ALB

Create new security group:

Name → medicare-alb-sg

Inbound rules:

Type	Port	Source
HTTP	80	0.0.0.0/0

📌 ALB accepts public traffic

9️⃣ Listener & Routing

Listener → HTTP : 80

Forward to → medicare-tg

Click Create load balancer

⏳ Wait until Status = Active



🧩 PART C: Attach ALB to Auto Scaling Group
🔟 Attach Target Group to ASG

EC2 → Auto Scaling Groups

Select medicare-asg

Go to Load balancing tab

Click Edit

Select:

✅ Application Load Balancer

Target group → medicare-tg

Save

⏳ ASG will now register instances automatically.

✅ Verification (VERY IMPORTANT)
🔹 Check Target Group Health

EC2 → Target Groups

Select medicare-tg

Go to Targets tab

You should see:

✅ EC2 instances

✅ Status = Healthy

🔹 Test Application

EC2 → Load Balancers

Copy ALB DNS name

Paste in browser

You should see:

MediCare Hub - Reliable EC2 Instance

🎉 SUCCESS

After creating the ALB:

I attached the target group to the Auto Scaling Group

EC2 instances were registered automatically

New instances launched by ASG are added automatically

This ensures:

Scaling does not require manual changes

Reliability is maintained at all times
🔁 Reliability in Action (What This Phase Proves)

With this setup:

If one EC2 instance fails → ALB stops sending traffic

Auto Scaling launches a replacement EC2

ALB starts sending traffic to the new healthy instance

Users experience no downtime

This is a self-healing traffic layer.

✅ Phase 03 Outcome (Summary)

After completing Phase 03:

The application has a single reliable entry point

Traffic is evenly distributed

Failed servers are automatically isolated

The system is resilient to instance-level failures

This phase removes single points of failure from the compute layer.
