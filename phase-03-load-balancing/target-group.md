I created a Target Group that defines:

Which EC2 instances receive traffic

How the load balancer checks instance health

The target group acts as a bridge between the ALB and the EC2 instances.

🔹 Why a target group is needed

The load balancer does not send traffic directly to EC2 instances.
Instead, it sends traffic to a target group, which:

Keeps track of registered EC2 instances

Continuously checks if instances are healthy

Automatically removes unhealthy instances

This ensures traffic is sent only to working servers.

🔹 Steps followed:

1️⃣ Create Target Group

AWS Console → EC2

Left menu → Target Groups

Click Create target group

🔹 Configuration

Target type → Instances

Target group name → medicare-tg

Protocol → HTTP

Port → 80

VPC → medicare-vpc

2️⃣ Health Check Settings (IMPORTANT)

Scroll to Health checks:

Protocol → HTTP

Path → /

Healthy threshold → 2

Unhealthy threshold → 2

Timeout → 5 seconds

Interval → 30 seconds

📌 This checks if Apache is running on EC2.

Click Next

3️⃣ Register Targets

Select NO instances manually

Click Create target group

📌 Auto Scaling Group will attach instances automatically.

🔹 Health Check Configuration

I configured health checks so AWS can automatically detect failures:

If an EC2 instance fails health checks:

It is marked Unhealthy

Traffic stops going to that instance
