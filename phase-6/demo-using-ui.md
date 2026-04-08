🚀**Phase-6: High Availability with MIGs and Load Balancing (GCP UI)**

🎯 **Goal**

Learn how to deploy a production-ready, highly available web application in GCP using Managed Instance Groups (MIGs), HTTP(S) Load Balancer, and health checks, with observability through Cloud Logging — all using the GCP Console (UI only).

## Key Concepts Covered

| Concept                | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| **Managed Instance Group** | Automatically manages identical VMs across zones                            |
| **Instance Template**     | Blueprint for creating VMs (OS, startup script, tags)                       |
| **HTTP(S) Load Balancer**  | Global load balancer with traffic distribution and health checks             |
| **Health Check**           | Continuously checks backend health to route traffic                          |
| **Multi-zone Deployment**  | Ensures high availability (HA) by distributing instances across zones        |
| **Cloud Logging**         | Logs backend traffic and health status for observability                     |

🧪**Hands-On Lab (Console UI Only)**

🛠️ **Step 1: Write Your Startup Script**

```bash
#!/bin/bash
apt update
apt install -y nginx
echo "Welcome to MIG Demo - $(hostname)" > /var/www/html/index.html
```

Save this script as startup.sh on your local machine.

🛠️**Step 2: Create an Instance Template**

Go to Compute Engine → Instance templates

Click Create instance template

Set:
Name: web-template
Machine type: e2-micro
Boot disk: Debian or Ubuntu

Under Advanced options → Automation → Startup script:

Paste the contents of startup.sh

Add network tag: http-server

Click Create

🛠️ **Step 3: Create a Managed Instance Group (MIG)**

Go to Compute Engine → Instance groups

Click Create instance group

Set:
Name: web-mig

Location: Multiple zones in us-central1

Select zones: us-central1-a, us-central1-b, us-central1-c

Instance template: web-template

Autoscaling: Enable (optional)

Number of instances: 3 (1 per zone)


Click Create

🛠️ **Step 4: Allow HTTP Traffic via Firewall**

Go to VPC network → Firewall

Click Create firewall rule

Set:

Name: allow-http

Direction: Ingress

Targets: Tags

Target tag: http-server

Source IP ranges: 0.0.0.0/0

Protocols: Allow TCP port 80


Click Create

🛠️** Step 5: Create a Health Check**

Go to Network services → Health checks

Click Create a health check

Set:

Name: web-health-check

Protocol: HTTP

Port: 80

Click Create

🛠️** Step 6: Create Backend Service and Attach MIG**

Go to Network services → Load balancing

Click Create load balancer → Start configuration

Choose:
HTTP(S) Load Balancer (From Internet to my VMs)

Set:

Name: web-lb

Backend configuration:

Create backend service

Add the MIG (web-mig)

Attach the health check (web-health-check)

Click Next

🛠️** Step 7: Configure URL Map and Frontend**

In the same wizard:

Leave URL map as default

Frontend:

Protocol: HTTP

Port: 80

Create a new global IP (name it web-ip)


Click Create

🛠️** Step 8: Access the Load Balancer**

Go to VPC → External IP addresses

Look for the web-ip you reserved earlier

Open it in a browser → You should see responses like:

Welcome to MIG Demo - web-xxxxx

🛠️ **Step 9: Enable Backend Logging**

Go to Network services → Load balancing

Click into web-lb

Click Edit backend service

Enable:

Cloud Logging

Set sample rate: 1.0 (100%)

Save changes

To view logs:

Go to Logging → Logs Explorer

Query:

resource.type="http_load_balancer"

📦** Real-World DevOps Use Case**

You need to deploy a frontend web app behind a highly available, globally accessible HTTP load balancer. It must:

Run across zones

Auto-heal unhealthy VMs

Log traffic for observability

✅ This setup mirrors how real-world production systems are deployed for uptime and scale.

✅ **Key Takeaways**

Use MIGs for auto-healing and cross-zone scaling

GCP’s HTTP Load Balancer is global, fast, and fully managed

Health checks remove bad instances from serving traffic

Logging adds visibility into real traffic and backend health

This is a foundational DevOps skill for building resilient cloud infra

