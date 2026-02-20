In this phase, I implemented load balancing for the MediCare Hub application.

The purpose of this phase was to ensure that:

User traffic is evenly distributed

No single EC2 instance becomes overloaded

Failed EC2 instances do not receive traffic

The application remains available even if servers fail

To achieve this, I used an Application Load Balancer (ALB) with health checks.

🔹 Why load balancing is important for reliability

Without a load balancer:

Users connect directly to one EC2 instance

If that instance fails → application goes down

Traffic spikes can crash the server

In a medical application:

Downtime is not acceptable

Traffic must be handled smoothly

Failures must be detected automatically

A load balancer solves this by acting as a single, reliable entry point to the application.

🔹 What I built in this phase

In Phase 03, I built:

A Target Group for EC2 instances

An Internet-facing Application Load Balancer

Health checks to monitor EC2 instance health

Integration with Auto Scaling Group
