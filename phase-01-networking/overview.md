In this phase, I designed the network foundation of the MediCare Hub application using Amazon Web Services (AWS).

The goal of this phase was to make sure that the application network:

Has no single point of failure

Can survive Availability Zone (AZ) failures

Separates public access from private backend resources

This networking layer is the base for all other reliability features like Auto Scaling, Load Balancer, RDS Multi-AZ, and EFS.

🔹 Why networking is important for reliability

In real-life terms:

If an entire building loses power, a hospital should still run from another building.

In AWS:

A single Availability Zone can fail

If everything is placed in one AZ → the application goes down

So, the network must be designed to:

Spread resources across multiple AZs

Allow public access only where required

Keep databases and servers private and secure

🔹 What I built in this phase

In Phase 01, I created:

A custom VPC

2 public subnets (for Application Load Balancer)

2 private subnets (for EC2 and RDS)

Subnets distributed across two Availability Zones

Internet Gateway and route tables

📌 This design ensures AZ-level isolation, which is a key principle of the AWS Reliability Pillar.
