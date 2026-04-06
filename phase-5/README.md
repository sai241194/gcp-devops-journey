**Phase-5:Google Cloud Storage and Related Services**

1.	**Google Cloud Storage (GCS)** – Object storage for unstructured data like logs, artifacts, and backups. 

2.	**Filestore** – Managed NFS file system for workloads requiring shared POSIX file access. 

3.	**Local SSD** – High-performance ephemeral block storage attached directly to VM hosts. 

4.	**Cloud Bigtable** – Wide-column NoSQL database for large-scale, time-series, and operational data. 

5.	**Pub/Sub** – Messaging and event streaming service for microservices communication.

## Related GCP Services Comparison

| Service | Type | Scope / Usage | Durability & Availability | Example Equivalent |
|---|---|---|---|---|
| Google Cloud Storage | Object Storage | Regional / multi-regional buckets | 99.999999999% durability | AWS S3, Azure Blob Storage |
| Filestore | File (NFS) | Shared file systems for VMs / GKE | Regional (zonal redundancy) | AWS EFS, Azure Files |
| Local SSD | Block (Ephemeral) | Ultra-fast temporary storage tied to VM | Tied to VM lifecycle | AWS Instance Store |
| Cloud Bigtable | NoSQL DB | Analytics, monitoring, time-series | Regional replication | AWS DynamoDB (similar) |
| Pub/Sub | Messaging Bus | Event-driven, async service communication | Global HA managed | AWS SQS/SNS, Kafka |

**DevOps Use Cases**

**Cloud Storage (GCS)**

•	Store CI/CD artifacts, Helm charts, and Terraform state files 

•	Centralized logging and backup storage for Kubernetes clusters 

•	Host static websites and internal documentation 

**Filestore**

•	Shared configuration for stateful Kubernetes workloads (e.g., Jenkins home) 

•	Persistent shared storage for legacy apps migrated to GKE 

**Local SSD**

•	High-performance cache for CI/CD pipelines 

•	Temporary ETL/data processing staging area

**Bigtable**

•	Long-term observability data (metrics, logs, traces) 

•	Backend for time-series monitoring tools 

**Pub/Sub**

•	Trigger pipelines based on events 

•	Stream logs/metrics to BigQuery or GCS

•	Incident automation with Cloud Functions and alerting tools 

•	Decouple microservices using asynchronous communication


**Hands-On Demo: Accessing GCS from a Compute Engine VM**

This demo shows how to securely connect GCS with a Compute Engine VM using the Console UI and Service Accounts.

**What You Will Learn**

•	Create and configure a GCS bucket 

•	Use Service Accounts for IAM-based access

•	Launch a VM with an attached Service Account

•	Access GCS from inside the VM 

•	Safely clean up resources 

**Step 1: Create a Project**

Create a new project: gcs-demo-bucket

**Step 2: Create a GCS Bucket**

•	Go to Cloud Storage → Buckets 

•	Click Create 

•	Bucket name: gcs-sai-bucket-demo-vm 

•	Region: asia-south1 (Mumbai)

•	Default storage class: Standard 

•	Upload a sample file: File.txt

**Step 3: Create a Service Account**

•	Go to IAM & Admin → Service Accounts 

•	Create: gcs-demo-sa 

•	Assign role: Storage Object Admin

**Step 4: Launch a Compute Engine VM**

•	Go to Compute Engine → VM Instances

•	Instance name: gcs-demo

•	Region: asia-south1 (Mumbai)

•	Zone: asia-south1-a 

•	Machine type: e2-micro 

.**Step 5: Access GCS from VM**

•	SSH into the VM from the console.

•	Use gcloud storage ls to list bucket files.

•	Download and upload files between VM and bucket
.

**Step 6: Cleanup (Very Important)**

•	Delete the VM 

•	Delete the bucket 

•	Delete the Service Account

OR 

•	Delete the entire project if created only for this demo 

Also ensure billing is disabled if not needed.



