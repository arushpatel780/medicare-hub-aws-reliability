I created a Route 53 hosted zone and configured DNS records to route user requests to the Application Load Balancer.

This setup makes the application:

Easier to access

More resilient to infrastructure changes

Ready for future failover scenarios

🔹 Why an Alias Record is important

Instead of using a static IP:

ALB IPs can change

Managing IP-based DNS becomes unreliable

An Alias record:

Automatically tracks the ALB

Requires no manual updates

Improves reliability and simplicity

This is a recommended AWS best practice.

🔹 Steps followed:

🧩 PART A: Create Hosted Zone
1️⃣ Go to Route 53

AWS Console → Search Route 53

Click Hosted zones

Click Create hosted zone

2️⃣ Hosted Zone Details

Domain name → medicarehub-demo.com
(any fake/demo domain is OK)

Type → Public hosted zone

Click Create hosted zone

📸 Screenshot hosted zone records

🧩 PART B: Create Alias Record to ALB
3️⃣ Create Record

Inside hosted zone → Create record

Record name → leave blank

Record type → A

Enable Alias

Alias target → Select ALB

Routing policy → Simple

Click Create records

🧩 PART C: Enable Health Checks (Optional but Advanced)

4️⃣ Create Health Check

Route 53 → Health checks

Create health check

Endpoint → ALB DNS

Protocol → HTTP

Path → /

📌 Used for DNS-level failover in production

🔹 Health Checks (Optional but Powerful)

I also explored Route 53 health checks, which:

Monitor application endpoints

Detect unhealthy resources

Can be used for DNS-level failover

While not required for basic routing, health checks add:

Another reliability layer

Support for multi-region or backup architectures



🔁 How Reliability Works Here (Simple Explanation)

When a user accesses the application:

DNS request goes to Route 53

Route 53 routes traffic to the ALB

ALB forwards traffic only to healthy EC2 instances

If the ALB endpoint changes:

DNS automatically adjusts

Users are not affected

This adds resilience at the entry point of the system.

⚠️ Cost Awareness (Important Note)

For learning and documentation:

The hosted zone and health checks were created temporarily

Screenshots were captured as proof

Resources were deleted afterward to control costs

This demonstrates cost-conscious architecture design.

✅ Phase 06 Outcome (Summary)

After completing Phase 06:

The application has a stable DNS entry point

Traffic routing is reliable and scalable

The architecture is ready for advanced failover scenarios

This completes the end-to-end reliability design of the system.
