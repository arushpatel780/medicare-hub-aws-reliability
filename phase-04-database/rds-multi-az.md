I created an Amazon RDS database instance with Multi-AZ enabled.

This means:

One primary database runs in one AZ

A standby database runs in another AZ

AWS continuously replicates data between them

If the primary database fails:

AWS automatically promotes the standby

The application continues using the same endpoint

🔹 Why Multi-AZ is needed

Multi-AZ solves critical reliability problems:

Protects against AZ-level failures

Removes the database as a single point of failure

Eliminates manual failover

Reduces downtime significantly

For a healthcare application, this is a must-have design choice.

🔹 How I did it (AWS Console)

Steps followed:
🧩 PART A: Create DB Subnet Group (REQUIRED)

RDS needs to know which private subnets it can use.

1️⃣ Create DB Subnet Group

AWS Console → Search RDS

Left menu → Subnet groups

Click Create DB subnet group

Fill details:

Name → medicare-db-subnet-group

Description → Private subnets for RDS Multi-AZ

VPC → medicare-vpc

Add subnets:

✅ private-subnet-1a

✅ private-subnet-1b

📌 Must be different AZs

Click Create

🧩 PART B: Create RDS Multi-AZ Database
2️⃣ Click Create Database

RDS → Databases

Click Create database

3️⃣ Choose Creation Method

Select → Standard create

4️⃣ Engine Selection

Choose ONE (both are fine):

✅ MySQL (simpler, very common)
OR

✅ PostgreSQL (also excellent)

👉 I recommend MySQL for clarity.

5️⃣ Templates

Select:

Production

📌 This unlocks Multi-AZ

6️⃣ Availability & Durability (IMPORTANT)

✅ Multi-AZ DB instance

📌 This is the heart of reliability.

7️⃣ DB Instance Settings

Set exactly this to minimize cost:

DB instance identifier → medicare-db

Master username → admin

Password → (store it safely)

8️⃣ Instance Configuration (VERY IMPORTANT)

DB instance class → db.t3.micro
(smallest available)

⚠️ Still paid, but cheapest.

9️⃣ Storage

Storage type → General Purpose (gp2/gp3)

Allocated storage → 20 GB

❌ Disable storage autoscaling

🧩 PART C: Connectivity (CRITICAL FOR SECURITY)
🔟 Network Settings

VPC → medicare-vpc

DB subnet group → medicare-db-subnet-group

Public access → ❌ NO

📌 This ensures DB is private only

1️⃣1️⃣ Security Group

Choose Existing security group

Select → medicare-ec2-sg

❌ Remove default SG

📌 This allows only EC2 → DB, not internet

1️⃣2️⃣ Database Authentication & Monitoring

Leave defaults

❌ Disable Performance Insights (to save cost)

1️⃣3️⃣ Create Database

Click Create database

⏳ Status will be:

Creating → Available

(wait 5–10 minutes)

✅ What to VERIFY (VERY IMPORTANT)

Once Available, open DB details and check:
| Setting             | Expected          |
| ------------------- | ----------------- |
| Multi-AZ            | **Yes**           |
| Publicly accessible | **No**            |
| Subnet group        | Private subnets   |
| Availability Zones  | Two different AZs |


🔹 Private Database Design (Very Important)

The database was placed in private subnets, which means:

It cannot be accessed from the internet

Only EC2 instances inside the VPC can connect

Security and reliability are improved

This reduces:

Attack surface

Risk of accidental exposure

Dependency on public networking
🔁 How Reliability Works Here (Simple Explanation)

If a database issue happens:

AWS detects the failure

Standby database is promoted automatically

Application reconnects using the same endpoint

Users experience little or no disruption

No manual action is required.

⚠️ Cost Awareness (Important Note)

For documentation and learning:

The RDS Multi-AZ database was created temporarily

Screenshots were taken as proof

The database was deleted immediately to control costs

This approach demonstrates:

Real-world knowledge

Cost responsibility

Practical AWS experience
After completing Phase 04:

The database layer has no single point of failure

Data is protected against AZ failures

Failover happens automatically

The application is ready for production-grade reliability

This phase secures the most critical component of the system.
