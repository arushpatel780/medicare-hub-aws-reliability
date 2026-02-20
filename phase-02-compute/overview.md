In this phase, I designed the compute layer of the MediCare Hub application.

The compute layer is responsible for:

Running the application code

Handling user requests

Automatically recovering if a server fails

To achieve reliability, I used:

EC2 Launch Template

Auto Scaling Group (ASG)

Deployment across multiple Availability Zones

This ensures the application is self-healing and scalable.

🔹 Why the compute layer is critical for reliability

In a traditional setup:

The application runs on one server

If that server crashes → the app goes down

In a real medical application:

Downtime can affect patients and doctors

Manual recovery is not acceptable

So the system must:

Automatically replace failed servers

Always keep the required number of servers running

Distribute servers across different AZs

This is exactly what Auto Scaling provides.

🔹 What I built in this phase

In Phase 02, I built:

An EC2 Launch Template (blueprint for servers)

An Auto Scaling Group

Minimum 2 EC2 instances running at all times

EC2 instances distributed across two AZs
