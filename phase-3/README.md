**Phase-03 — IAM Roles, Permissions and Best Practices in Google Cloud Platform**

**Learning Objectives**

•	Understand what IAM is and why it is important

•	Learn IAM core components: Identity, Role, Policy, Resource

•	Understand Types of Roles: Basic, Predefined, Custom

•	Learn IAM hierarchy and permission inheritance

•	Grant limited access to a junior teammate (real use-case)

•	Understand Service Accounts for DevOps automation

•	Follow IAM best practices and least privilege principle

**What is IAM in GCP?**

IAM (Identity and Access Management) is the framework that controls who can do what on which resource.

Formula: Who → Can do what → On which resource

Authentication → Who are you? (Users/Groups/Service Accounts)

Authorization → What can you do? (Roles/Permissions)

## Core IAM Components

| Component | Description |
|-----------|-------------|
| Identity  | A user, group, domain, or service account |
| Role      | A collection of permissions |
| Policy    | Binding of identity to a role |
| Resource  | Project, VM, Bucket, Database, etc. |

## Types of IAM Roles

| Role Type        | Description                              | Example                 |
|------------------|------------------------------------------|-------------------------|
| Basic Roles      | Broad, legacy roles (not recommended)    | Owner, Editor, Viewer  |
| Predefined Roles | Fine-grained, service-specific           | roles/storage.admin    |
| Custom Roles     | User-defined permissions                 | compute.instances.start|

**IAM Policy Hierarchy**

•	Organization

•	Folder

•	Project

•	Resource

Note: Permissions inherit from parent to child unless explicitly overridden.


**IAM Best Practices for DevOps**

•	Follow Least Privilege principle

•	Avoid Basic Roles

•	Use Service Accounts for automation

•	Rotate keys and secrets regularly

•	Audit IAM permissions frequently


🧪 **Practical Task**

🔧 **Practical Task 1:Create Project & Assign Viewer Role** 

export PROJECT_ID="devops-iam-demo-$(date +%s)"
gcloud projects create $PROJECT_ID
gcloud config set project $PROJECT_ID

gcloud projects add-iam-policy-binding $PROJECT_ID \
  --member="user:devops.engineer@example.com" \
  --role="roles/viewer"












