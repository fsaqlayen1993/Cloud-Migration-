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
- Amazon EC2 (VM Import/Export + AMI + Instance):the core migration service.