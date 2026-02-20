I created four subnets inside the VPC:

| Subnet Type      | Availability Zone | Purpose       |
| ---------------- | ----------------- | ------------- |
| Public Subnet 1  | AZ-a              | Load Balancer |
| Public Subnet 2  | AZ-b              | Load Balancer |
| Private Subnet 1 | AZ-a              | EC2 / RDS     |
| Private Subnet 2 | AZ-b              | EC2 / RDS     |

🔹 Why multiple subnets across AZs are needed

If all resources are in one AZ:

AZ failure = full application downtime

By using multiple AZs:

Load balancer remains available

EC2 instances can be launched in healthy AZs

Databases can fail over safely

This is a core reliability design principle.



Steps:
[1] Create Public Subnet 1 (AZ-a)
🔹 Steps

Left menu → Subnets

Click Create subnet

🔹 Configuration

VPC → medicare-vpc

Subnet name → public-subnet-1a

Availability Zone → us-east-1a

IPv4 CIDR → 10.0.1.0/24

📌 Click Create subnet

[2] Create Public Subnet 2 (AZ-b)

Repeat the same steps:

Subnet name → public-subnet-1b

Availability Zone → us-east-1b

IPv4 CIDR → 10.0.2.0/24

📌 Click Create subnet

✅ Why 2 public subnets?

ALB requires at least two AZs

If one AZ fails → traffic still flows

[3] Create Private Subnet 1 (AZ-a)
🔹 Steps

Click Create subnet again

🔹 Configuration

Subnet name → private-subnet-1a

Availability Zone → us-east-1a

IPv4 CIDR → 10.0.3.0/24

📌 Click Create subnet

[4] Create Private Subnet 2 (AZ-b)

Again:

Subnet name → private-subnet-1b

Availability Zone → us-east-1b

IPv4 CIDR → 10.0.4.0/24

📌 Click Create subnet

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
