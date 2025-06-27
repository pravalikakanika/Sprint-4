

![image](https://github.com/user-attachments/assets/445e995f-5b72-4bcd-b44a-0623949ae268)

# POC of Terraform Drift

|**Author**        | **created on**       | **Version** |**Last edited on**| **Review Level**   | **Reviewer**      |
|---------------|------------|---------|--------|--------|----------------------|
| Pravalika Kanikarapu  | Jun 27  | v1.0|   Jun 27  | Pre-Reviewer   | Priyanshu            |
| Pravalika Kanikarapu  |  |  |   | L0             | Priyanka     |
| Pravalika Kanikarapu  |      |      |         | L1             | Rishabh Sharma       |
| Pravalika Kanikarapu  |      |      |         | L2             | Piyush Upadhyay      |



# Table of Contents

- [Introduction](#introduction)
- [System Requirements](#system-requirements)
- [Prerequisites](#prerequisites)
- [Ports Required](#ports-required)
- [Step-by-step Demo Script](#step-by-step-demo-script)
- [Conclusion](#conclusion)
- [Contact Information](#contact-information)
- [References](#references)




# Introduction

This documentation is about Drift detection, how Terraform detects drift between the declared infrastructure (.tf files) and actual state in the cloud.

For more information related follow this link[Terraform Drift Documentation](https://github.com/Cloud-NInja-snaatak/Documentation/tree/Kanika-SCRUM-353/terraform/drift/documentation)

# System Requirements

| Component        | Minimum Requirement           |
|------------------|-------------------------------|
| OS               | Ubuntu or other Linux-based   |
| Disk Space       | 8 GB                         |
| RAM              | 2 GB                          |
| Processor        | Single-core                     |
| Instance Type    | t2.small                      |

# Prerequisites

| **Category**                    | **Requirement**                                                                    |
| ------------------------------- | ---------------------------------------------------------------------------------- |
| **Terraform Setup**             | Terraform CLI installed (v1.0+ recommended)                                        |
| **Cloud Provider**              | A configured cloud account (e.g., AWS, Azure, GCP) with sufficient permissions     |
| **Authentication**              | Access credentials configured (`aws configure`, environment variables, etc.)       |
| **Infrastructure Code**         | A valid Terraform project with `.tf` files and at least one resource defined       |
| **Manual Access**               | Console/portal access to manually change resources (to simulate drift)             |


# Ports Required

| Port | Used By     | Description                                      |
|------|-------------|--------------------------------------------------|
| 22   | SSH         | Used for secure remote login and VM access.     |



# Step-by-step demo script

## Clone or create a working directory
```
mkdir terraform-drift-poc
cd terraform-drift-poc
```

## Create main.tf
```
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "example" {
  bucket = "terraform-drift-poc-unique12345" # Use a unique name!
  tags = {
    Environment = "POC"
  }
}
```

##  Initialize Terraform
```
terraform init
```
![image](https://github.com/user-attachments/assets/5427bde7-9e12-4a34-b86a-48b25de343d7)


##  Apply infrastructure
```
terraform apply -auto-approve
```
![image](https://github.com/user-attachments/assets/2d40eaa1-07c4-4d0d-91f7-afb8f38037ad)


## Verify

- Go to AWS Console → S3 → Find your bucket

- Check that the tag Environment = POC is present

![image](https://github.com/user-attachments/assets/4dc15f24-14e9-4bd7-b9c4-823ee8761d35)


##  Create drift manually
  
- In AWS console, remove the Environment tag or change it to Test

![image](https://github.com/user-attachments/assets/860bd8df-5a15-4581-8c15-b4e37aafc4ed)


  ## Detect drift
```
terraform plan
```
![image](https://github.com/user-attachments/assets/480a82f6-12a0-4f7c-ab31-3eff5cf5ee54)

### Expected output:
```
~ resource "aws_s3_bucket" "example" {
      tags = {}
        -> Environment = "POC"
    }
```


##  Fix drift
```
terraform apply -auto-approve
```


![image](https://github.com/user-attachments/assets/9383913d-2cda-4f7d-9ca9-acff6f85e468)


![image](https://github.com/user-attachments/assets/5d9aff1f-89bd-4cfc-bef7-cd611956a86a)


# Conclusion

This POC demonstrates that Terraform can reliably detect **drift** between the declared infrastructure in `.tf` files and the actual state in the cloud. By simulating a manual change (e.g., modifying or removing a tag), and then running `terraform plan`, we clearly observe Terraform’s ability to recognize discrepancies.

Key outcomes:
-  Drift detection using standard `terraform plan` is straightforward and effective.
-  Manual infrastructure changes outside Terraform are flagged as deviations.
-  Drift can be corrected seamlessly using `terraform apply`.

This reinforces the importance of **Infrastructure as Code (IaC)** and highlights the value of regularly running `terraform plan` in CI pipelines to monitor and maintain infrastructure integrity.



# Contact Information

| Name         | Email Address                                 |
|--------------|-----------------------------------------------|
| Pravalika  | kanikarapu.pravalika.snaatak@mygurukulam.co|

# References
| Links                                             | Descriptions                                                    |
|---------------------------------------------------|-----------------------------------------------------------------|
|[Terraform Drift Documentation](https://github.com/Cloud-NInja-snaatak/Documentation/tree/Kanika-SCRUM-353/terraform/drift/documentation) |Documentation |
