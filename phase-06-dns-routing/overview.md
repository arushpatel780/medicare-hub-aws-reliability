In this phase, I implemented DNS-level routing for the MediCare Hub application using Amazon Route 53.

The goal of this phase was to:

Provide a stable and user-friendly entry point to the application

Route traffic reliably to the Application Load Balancer

Add another layer of availability and reliability at the DNS level

Even if infrastructure components change, users should always access the application through a single domain name.

🔹 Why DNS matters for reliability

Without proper DNS management:

Users must remember IP addresses or long ALB DNS names

If infrastructure changes, users may face downtime

Failover and health-based routing are not possible

DNS is the first point of contact for users.
If DNS is unreliable, the entire application becomes unreliable.

Route 53 solves this by offering:

Highly available DNS

Health checks

Tight integration with AWS services

🔹 What I built in this phase

In Phase 06, I implemented:

A public hosted zone

An alias record pointing to the Application Load Balancer

(Optional) Health checks for endpoint monitoring

This ensures traffic is always routed to a healthy application endpoint.
