In this phase, I implemented shared and durable storage for the MediCare Hub application using Amazon Elastic File System (EFS).

The goal of this phase was to ensure that:

Application data is not tied to a single EC2 instance

Data remains available even if an EC2 instance is terminated

Newly launched EC2 instances can immediately access existing data

This is an important reliability requirement for applications running on Auto Scaling Groups.

🔹 Why shared storage is important for reliability

In a basic EC2 setup:

Each EC2 instance has its own local storage

If the instance is terminated → data is lost

New instances start with empty storage

In a real application:

User uploads

Reports

Logs

Shared application files

must persist across instance failures.

Shared storage solves this problem.

🔹 What I built in this phase

In Phase 05, I implemented:

An Amazon EFS file system

Mount targets in multiple Availability Zones

Secure access from EC2 instances

Automatic mounting of EFS on EC2 startup

This ensures data durability and availability, independent of EC2 lifecycle events.
