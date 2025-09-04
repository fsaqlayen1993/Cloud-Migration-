# Cloud-Migration-

---
![alt text](image-1.png)
---

# Overview Of Cloud Migration
A basic part of cloud computing is learning how to move applications from local computers or servers to the cloud. On AWS, you can use Amazon EC2 to create and run virtual machines online. EC2 has a VM Import/Export feature that makes it easy to bring in virtual machine images from your current setup and run them in the cloud. However, once you export an application from VirtualBox, it won’t be available to use on your computer at that time, so you should be careful when doing the migration.

# Zone
US-East-1(North Virginia)

# Services:
- Oracle VirtualBox (local, no cost if you already have it).
- Amazon S3: for temporary storage of the OVA.
- AWS IAM: for secure roles & permissions (no cost).
- Amazon EC2 (VM Import/Export + AMI + Instance): the core migration service.

# Project Explanation:
## Export VM from VirtualBox:
- You start with an on-premise VirtualBox VM.

- Shut it down, then export it to an OVA/OVF format (Open Virtualization Format).

- This makes it portable for cloud migration.
## Upload VM Image to Amazon S3:
- Use the AWS CLI (aws s3 cp ...) to upload your .ova file into an S3 bucket.

- S3 acts as the temporary storage for the VM before it’s converted into an AMI.
## Set Up IAM Role for VM Import/Export:
- Create an IAM role with permissions for:
  Amazon S3 (read/write)
  Amazon EC2 (import/export)
  AWS KMS (if your file is encrypted)

- This role allows AWS to perform the VM conversion on your behalf.
## Convert OVA → AMI:
- Use EC2 VM Import/Export to import the .ova file from S3.

- AWS processes the file and creates an Amazon Machine Image (AMI), which is like a template for launching EC2 instances.
## Launch EC2 Instance:
- Provision a new EC2 instance using the AMI created.

- You now have your VirtualBox VM running as a cloud-based virtual machine inside AWS.


# Pricing Breakdown (as of 2025, AWS standard rates):
## Amazon S3 (storing VM image):
- Storage: ~$0.023/GB per month (Standard Tier).

- Example: A 20 GB OVA file = $0.46/month.

- Data Transfer IN: Free (uploading to S3).

- Data Transfer OUT (if downloading back): ~$0.09/GB.
## VM Import/Export:
- No additional fee for importing VMs into EC2 (AWS only charges for the underlying resources: S3, EC2, EBS).
## EC2 Instance (after import):
- Pricing depends on instance type + region.
Example (US East 1):
- t3.medium (2 vCPU, 4 GiB RAM): $0.0416/hour (~$30/month if always running).

- t3.large (2 vCPU, 8 GiB RAM): $0.0832/hour (~$60/month).

- If you run 24/7, costs accumulate. If you stop instances when not needed, you only pay for storage.
## EBS Volumes (backing EC2):
- ~$0.10/GB per month (General Purpose SSD gp3).

- Example: A 30 GB root volume = $3/month.
## IAM:
- Free (no charge for IAM users/roles/policies).
## Example Total Monthly Cost (for 1 migrated VM, ~20 GB image, t3.medium instance)
- S3 Storage: $0.46/month

- EBS Storage: $3.00/month

- EC2 Instance (t3.medium 24/7): ~$30.00/month

- IAM: Free
- ✅ Total ≈ $33–$35/month per VM