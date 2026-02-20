I configured routing to control who can access the internet.

I created:

An Internet Gateway (IGW)

A public route table

A private route table

🔹 Why route tables and IGW are needed

Public subnets must reach the internet (for ALB)

Private subnets must stay protected

Mixing both leads to security and reliability risks

This separation ensures:

Backend systems are not exposed

Only controlled entry points exist


Steps:

Created an Internet Gateway

Attached it to medicare-vpc

Created public route table

Added route: 0.0.0.0/0 → IGW

Associated public subnets to public route table

Created private route table

No internet route added

Create Internet Gateway (IGW)
🔹 Steps

Left menu → Internet Gateways

Click Create internet gateway

Name → medicare-igw

Click Create

🔹 Attach to VPC

Select IGW

Click Actions → Attach to VPC

Select medicare-vpc

Attach

✅ This allows public subnets to access the internet.

Create Public Route Table
🔹 Steps

Left menu → Route Tables

Click Create route table

🔹 Configuration

Name → public-rt

VPC → medicare-vpc

📌 Click Create

🔹 Add Internet Route

Select public-rt

Go to Routes tab

Click Edit routes

Add route:

Destination → 0.0.0.0/0

Target → Internet Gateway (medicare-igw)

Save

🔹 Associate Public Subnets

Go to Subnet associations

Click Edit subnet associations

Select:

public-subnet-1a

public-subnet-1b

1️⃣ Allocate Elastic IP (Required)
🔹 Steps

AWS Console → VPC

Left menu → Elastic IPs

Click Allocate Elastic IP

Click Allocate

✅ Leave it unassociated for now

📸 Screenshot this page (for GitHub)

2️⃣ Create NAT Gateway ⚠️ (PAID RESOURCE)
🔹 Steps

Left menu → NAT Gateways

Click Create NAT Gateway

🔹 Configuration

Name → medicare-nat-gateway

Subnet → public-subnet-1a
(must be public)

Connectivity type → Public

Elastic IP → Select the one you just created

📌 Click Create NAT Gateway

8️⃣ Private Route Table (NO Internet – Free Tier Safe)
🔹 Steps

Create another route table

Name → private-rt

VPC → medicare-vpc

📌 Click Create

Click Edit routes

Add route:
| Destination | Target      |
| ----------- | ----------- |
| 0.0.0.0/0   | NAT Gateway |

Save routes

Outcome (Summary):

The network supports multi-AZ reliability

Public and private access is clearly separated

The architecture is ready for:

Auto Scaling

Load Balancer

RDS Multi-AZ

EFS

This phase lays the foundation for a self-healing system.
