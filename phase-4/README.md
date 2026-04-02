**Phase-4: GCP Compute Engine (VMs, SSH, Images, Firewall)**

**•	Launch VMs, connect via SSH**

**•	Install packages via startup scripts**

•	**Create and use custom images**

•	**Enable firewall rules for external access**

**What is Compute Engine?**

•	Compute Engine provides on-demand virtual servers in Google Cloud, forming the IaaS foundation for running workloads. 

•	You can tailor each VM’s resources such as vCPU, memory, operating system, storage disks, and network settings to match application needs. 

•	It enables automation with startup scripts, reusable machine images, managed instance groups, and self-healing capabilities for high availability.

## Key Concepts

| Concept        | Description                                                         |
|----------------|---------------------------------------------------------------------|
| Instance       | A VM (virtual server) that runs in a GCP zone                      |
| Zone           | A single data center in a GCP region                               |
| Machine Type   | Defines CPU and RAM (e.g., e2-micro, n1-standard-1)                |
| Boot Disk      | Persistent disk attached to the VM that contains the OS            |
| Startup Script | Script that runs automatically when the VM starts                   |
| Firewall Rule  | Controls allowed network traffic to and from the VM                |


🧪 **Hands-On Lab**

**Launch a VM and Connect via SSH Using CLI:**

```bash
gcloud compute instances create my-first-vm \
  --zone= asia-south1-a \
  --machine-type=e2-micro \
  --image-family=ubuntu-2004-lts \
  --image-project=ubuntu-os-cloud \
  --tags=http-server

# SSH into the instance

gcloud compute ssh my-first-vm --zone= asia-south1-a
```


**Manually Install NGINX on Ubuntu VM:**

Once inside the VM via SSH, run the following:

```bash
sudo apt update
sudo apt install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx
sudo systemctl status nginx
ps -aux|grep nginx
```

**To test:**

```bash
curl http://localhost
```

**Install NGINX Automatically via Startup Script:**

```bash
gcloud compute instances create nginx-vm \
  --zone= asia-south1-a \
  --machine-type=e2-micro \
  --image-family=ubuntu-2004-lts \
  --image-project=ubuntu-os-cloud \
  --metadata startup-script='#! /bin/bash
apt update
apt install -y nginx
systemctl enable nginx
systemctl start nginx' \
  --tags=http-server
```

**Enable Firewall Rule for HTTP Access:**

```bash
gcloud compute firewall-rules create allow-http \
  --allow tcp:80 \
  --target-tags=http-server \
  --description="Allow HTTP traffic" \
  --direction=INGRESS \
  --priority=1000 \
  --network=default
```


**Create a Custom Image from Existing VM:**

# Stop the VM before creating image

```bash
gcloud compute instances stop nginx-vm --zone= asia-south1-a
```

# Create image from disk

```bash
gcloud compute images create nginx-custom-image \
  --source-disk=nginx-vm \
  --source-disk-zone= asia-south1-a
```

# Launch a new VM from custom image

```bash
gcloud compute instances create nginx-from-image \
  --zone= asia-south1-a \

  --machine-type=e2-micro \
  --image=nginx-custom-image \
  --tags=http-server
```

**Real-World DevOps Use Case**

Suppose you need to:

•	Provision a VM that installs NGINX automatically at launch 

•	Make the application reachable from the internet 

•	Create a reusable base setup for future environments and CI/CD use 


**Approach:**
✅ Use startup scripts to install and configure software during VM boot
✅ Configure firewall rules to allow HTTP access from outside
✅ Create a custom image from the configured VM for consistent reuse

**Key Learnings**

•	Compute Engine provides virtual machines as part of GCP’s IaaS model. 

•	Startup scripts help achieve automated, repeatable server configuration. 

•	Custom images ensure standardized environments across deployments. 

•	Proper firewall configuration is required for external connectivity. 

•	VM provisioning should be automated using gcloud CLI or Terraform for DevOps efficiency. 
















