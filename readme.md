

![image](https://github.com/user-attachments/assets/445e995f-5b72-4bcd-b44a-0623949ae268)

# POC of Terraform Drift

|**Author**        | **created on**       | **Version** |**Last edited on**| **Review Level**   | **Reviewer**      |
|---------------|------------|---------|--------|--------|----------------------|
| Pravalika Kanikarapu  | Jun 27  | v1.0|   Jun 27  | Pre-Reviewer   | Priyanshu            |
| Pravalika Kanikarapu  |  |  |   | L0             | Priyanka     |
| Pravalika Kanikarapu  |      |      |         | L1             | Rishabh Sharma       |
| Pravalika Kanikarapu  |      |      |         | L2             | Piyush Upadhyay      |

# Introduction

This documentation is about Drift detection, how Terraform detects drift between the declared infrastructure (.tf files) and actual state in the cloud.

## System Requirements

| Component        | Minimum Requirement           |
|------------------|-------------------------------|
| OS               | Ubuntu or other Linux-based   |
| Disk Space       | 8 GB                         |
| RAM              | 2 GB                          |
| Processor        | Single-core                     |
| Instance Type    | t2.small                      |

## Prerequisites

| **Category**                    | **Requirement**                                                                    |
| ------------------------------- | ---------------------------------------------------------------------------------- |
| **Terraform Setup**             | Terraform CLI installed (v1.0+ recommended)                                        |
| **Cloud Provider**              | A configured cloud account (e.g., AWS, Azure, GCP) with sufficient permissions     |
| **Authentication**              | Access credentials configured (`aws configure`, environment variables, etc.)       |
| **Infrastructure Code**         | A valid Terraform project with `.tf` files and at least one resource defined       |
| **Manual Access**               | Console/portal access to manually change resources (to simulate drift)             |


## Ports Required

| Port | Used By     | Description                                      |
|------|-------------|--------------------------------------------------|
| 22   | SSH         | Used for secure remote login and VM access.     |



## Commands to setup

### 1. Update Package Index

**Follow Step 3 here**: [Ubuntu Basic System Commands](https://github.com/snaatak-Downtime-Crew/Documentation/tree/main/common_stack/operating_system/ubuntu/sop/commoncommands#1-basic-system-commands)


### 2.  Install Terraform 
```
sudo apt-get install -y gnupg software-properties-common curl
```
#### Add HashiCorp GPG key
```
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
```
#### Add HashiCorp repo
```
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
  sudo tee /etc/apt/sources.list.d/hashicorp.list
```
#### Install Terraform
```
sudo apt update && sudo apt install terraform
```
#### Check version
```
terraform version
```
![Screenshot 2025-06-23 214229](https://github.com/user-attachments/assets/750c6629-a978-4bf8-9818-469e33b50e9b)



### 3. Create an Infra using Terraform

#### Create Terraform module
![Screenshot 2025-06-23 214544](https://github.com/user-attachments/assets/9088b578-b6dc-4f4e-a8ec-21d6e435b1ea)


### 4. Run Terraform Commands

```
terraform init  
```
It initializes a working directory that contains Terraform configuration files. 
- Downloads the necessary provider plugins (e.g., AWS, Azure, Google Cloud).
- Sets up the remote backend (like S3, local, etc.) for storing the state file.
- Sets up the .terraform/ directory for use with plan, apply, etc.

Terraform creates a .terraform folder which contains:
Provider binaries
Backend configuration
Lock file (.terraform.lock.hcl) to pin plugin versions
![Screenshot 2025-06-23 215324](https://github.com/user-attachments/assets/93fb7b33-5ef7-4e55-9da7-cae892eae340)


```
terraform validate
```
It validates that your configuration files are syntactically and logically correct.
![Screenshot 2025-06-23 215431](https://github.com/user-attachments/assets/c9a30cbd-51f1-4460-b023-7a0625ebfd0d)


```
terraform plan 
```
Shows what changes Terraform will make to match your config with the actual infrastructure 

![Screenshot 2025-06-23 123016](https://github.com/user-attachments/assets/bf99c7c8-d1ab-4b4f-bce6-d38e174a42a1)


```
terraform apply -auto-approve
```
![Screenshot 2025-06-23 220027](https://github.com/user-attachments/assets/4e7189fb-382b-463e-9c33-6f773352b284)



## Conclusion

Use terraform plan -detailed-exitcode in Jenkins. It is:
Simple
Fast to integrate
Free
CI/CD-friendly
No new tools to maintain

## Contact Information

| Name         | Email Address                                 |
|--------------|-----------------------------------------------|
| Pravalika  | kanikarapu.pravalika.snaatak@mygurukulam.co|

### References
| Links                                             | Descriptions                                                    |
|---------------------------------------------------|-----------------------------------------------------------------|
|[Link](https://github.com/snaatak-Downtime-Crew/Documentation/blob/SCRUMS-388-Adil/Terraform/drift/doc/README.md) |Documentation |
