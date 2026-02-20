I created a custom Virtual Private Cloud (VPC) to host all application resources.

Instead of using the default VPC, I created my own so that I could:

Fully control IP ranges

Design my own subnets

Apply reliability best practices

🔹 Why a custom VPC is needed

Using a custom VPC helps because:

Default VPCs are shared and generic

Production systems need controlled and isolated networking

Reliability designs require intentional subnet placement

Without a custom VPC:

You cannot properly design multi-AZ architectures

Network-level reliability becomes limited



🔹 Steps

Go to AWS Console

Search → VPC

Click Your VPCs

Click Create VPC

🔹 Select

Resources to create → VPC only

Name tag → medicare-vpc

IPv4 CIDR block → 10.0.0.0/16

IPv6 CIDR → ❌ None

Tenancy → Default

📌 Click Create VPC

✅ Why this matters (Reliability)

Isolated network

Full control over subnets and AZ placement
