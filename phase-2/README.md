**Phase-02 — GCP Project and Billing Management**

**Learning Objectives**

• What is the GCP hierarchy

• What is a Project and why it is important

• How Billing Accounts work in GCP

• How to set Budget alerts to avoid unexpected charges

• How to enable required APIs before using services

**GCP Hierarchy**

In GCP, resources are organized in this hierarchy:
 


Everything you create must be inside a Project. You cannot create resources without a project.

**What is a GCP Project?**

A Project is like a separate workspace where all your cloud resources live.

Inside a project, you manage:

• Virtual Machines

• Storage Buckets

• Databases

• IAM permissions

• API access

• Billing usage

Each project has its own billing, IAM roles, APIs, and resources.
Multiple projects can share the same billing account.

**Billing Account in GCP**

When you sign up for GCP free tier, a billing account is automatically created and linked to your default project.

**Important Points:**

• One billing account can be linked to multiple projects
• Budget alerts can be set to track spending
• GCP does not stop services automatically when budget is reached

**Step 1: Create a New Project**

1. Open https://console.cloud.google.com
2. Click the Project dropdown at the top
3. Click **New Project**
4. Give the name: payments-dev
5. Select your billing account
6. Click Create

This project will be used for all upcoming labs.


**Step 2: Set Budget Alerts**

1. Go to Billing → Budgets & alerts
2. Click **Create Budget**
3. Set a budget limit (example: ₹1000)
4. Configure email alerts at 50%, 90%, and 100%
Note: Alerts only notify you. They do not stop services.

**Step 3: Enable Required APIs**
**APIs to enable:**

• Compute Engine API

• Cloud Storage API

• Cloud Logging API

• Cloud Monitoring API

• Cloud Resource Manager API

• IAM Service Account Credentials API

**Steps:**
1.	Go to **APIs & Services → Library**
2.	Search each API by name and click **Enable**
Alternatively, use Cloud Shell:


gcloud services enable compute.googleapis.com \
    storage.googleapis.com \
    monitoring.googleapis.com \
    logging.googleapis.com \
    cloudresourcemanager.googleapis.com \
    iamcredentials.googleapis.com







