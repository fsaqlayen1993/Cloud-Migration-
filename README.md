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