In this phase, I designed a reliable database layer for the MediCare Hub application using Amazon Web Services RDS with Multi-AZ deployment.

The database layer is responsible for:

Storing patient and application data

Ensuring data is always available

Protecting against failures at the infrastructure level

Since this is a medical application, database reliability is extremely critical.

🔹 Why the database layer is a reliability risk

In a basic setup:

There is only one database

If that database fails → application stops working

Manual recovery takes time and risks data loss

This creates a single point of failure, which is unacceptable for:

Medical systems

Production-grade applications

High-availability architectures

So the database must be designed to fail over automatically.

🔹 What I built in this phase

In Phase 04, I implemented:

A Multi-AZ RDS database

A private database setup (no public access)

Database subnets across multiple Availability Zones

Secure access from EC2 only

This ensures automatic database failover with minimal downtime.
