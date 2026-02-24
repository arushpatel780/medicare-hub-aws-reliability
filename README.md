MediCare Hub – AWS Reliability Architecture

A hands-on AWS project focused on designing a highly available, fault-tolerant, and self-healing architecture for a medical application using Amazon Web Services (AWS) Reliability Pillar best practices.

This project demonstrates how to eliminate single points of failure, handle infrastructure failures automatically, and build production-grade reliability.

Project Summary

MediCare Hub is a conceptual medical web application that originally lacked fault tolerance.
Any failure in servers, database, or network could lead to application downtime and data unavailability.

In this project, I redesigned the system using AWS Reliability Pillar principles by implementing:

Multi-AZ architecture

Auto Scaling and self-healing compute

Load balancing with health checks

Multi-AZ database

Shared storage

DNS-level routing

The final result is a highly available and resilient system capable of recovering automatically from failures.

Problem Statement

The original MediCare Hub architecture had single points of failure, such as:

A single EC2 instance

A single database instance

No load balancer

No automatic recovery mechanism

This meant:

If the server failed → application went down

If the database failed → data became unavailable

Manual intervention was required to recover

For a medical application, this level of risk is unacceptable.

What I Built

To solve these problems, I built a reliability-focused AWS architecture that includes:

A custom VPC with public and private subnets across multiple Availability Zones

EC2 instances managed by an Auto Scaling Group

An Application Load Balancer to distribute traffic and monitor health

A Multi-AZ RDS database for automatic failover

Amazon EFS for shared and durable storage

Route 53 for DNS-level routing and availability

Each layer of the system is designed to fail gracefully and recover automatically.

Why Reliability Matters

Reliability is critical because:

Infrastructure failures are inevitable

Systems must recover without manual intervention

Downtime can impact users, trust, and business operations

Medical systems must ensure continuous availability

This project follows key reliability principles:

No single point of failure

Automatic failover

Health monitoring

Multi-AZ deployment

Self-healing infrastructure

🖼️ Architecture Diagram

The diagram below represents the final reliable architecture of the MediCare Hub application:

📌 Location:

architecture/architecture-diagram.png

The diagram shows:

Multi-AZ VPC design

Application Load Balancer

Auto Scaling EC2 instances

Multi-AZ RDS database

Amazon EFS

Route 53 routing

☁️ AWS Services Used

The following AWS services were used to implement this project:

Amazon VPC – Network isolation and control

Amazon EC2 – Application servers

EC2 Launch Template – Standardized instance configuration

Auto Scaling Group – Self-healing and scaling

Application Load Balancer (ALB) – Traffic distribution and health checks

Amazon RDS (Multi-AZ) – Reliable relational database

Amazon EFS – Shared and durable file storage

Amazon Route 53 – DNS routing and health checks

📂 Project Documentation Structure

📑 Repository Navigation (Documentation Flow)

This project is documented step by step, following the exact order in which the architecture was designed and built.

1️⃣ Architecture Overview

📁 Architecture

📄 Architecture Explanation

🖼️ Architecture Diagram (architecture/architecture-diagram.png)

2️⃣ Phase 01 – Networking Foundation

📁 phase-01-networking

📄 Overview

📄 VPC Creation

📄 Subnet Setup (Multi-AZ)

📄 Route Tables & Internet Gateway

📸 Screenshots (phase-01-networking/screenshots/)

3️⃣ Phase 02 – Compute Layer (EC2 & Auto Scaling)

📁 phase-02-compute

📄 Overview

📄 EC2 Launch Template

📄 Auto Scaling Group

📸 Screenshots (phase-02-compute/screenshots/)

4️⃣ Phase 03 – Load Balancing

📁 phase-03-load-balancing

📄 Overview

📄 Target Group Configuration

📄 Application Load Balancer

📸 Screenshots (phase-03-load-balancing/screenshots/)

5️⃣ Phase 04 – Database Layer (RDS Multi-AZ)

📁 phase-04-database

📄 Overview

📄 RDS Multi-AZ Setup

📸 Screenshots (phase-04-database/screenshots/)

6️⃣ Phase 05 – Shared Storage (Amazon EFS)

📁 phase-05-shared-storage

📄 Overview

📄 Amazon EFS Setup

📸 Screenshots (phase-05-shared-storage/screenshots/)

7️⃣ Phase 06 – DNS & Routing (Route 53)

📁 phase-06-dns-routing

📄 Overview

📄 Route 53 Setup
phase-06-dns-routing/route53-setup.md

📸 Screenshots (phase-06-dns-routing/screenshots/)

8️⃣ Failure Testing (Reliability Proof)

📁 failure-testing

📄 Overview

📄 EC2 Failure & Auto Scaling Test

📄 ALB Health Check Test

📸 Screenshots (failure-testing/screenshots/)

9️⃣ Cleanup & Cost Control

📁 cleanup-and-cost-control

📄 Resources Created

📄 Resources Deleted (Cost Control)
⚠️ Cost Awareness Note

Some AWS services used in this project (such as ALB, NAT Gateway, RDS Multi-AZ, and EFS) were created temporarily for learning and documentation and deleted immediately to remain cost-efficient.

✅ Final Note

This project demonstrates hands-on experience with AWS Reliability Pillar, real-world architectural thinking, and cost-conscious cloud design.
