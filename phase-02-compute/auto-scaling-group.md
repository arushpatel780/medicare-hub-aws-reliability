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
