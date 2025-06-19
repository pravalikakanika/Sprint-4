
![image](https://github.com/user-attachments/assets/445e995f-5b72-4bcd-b44a-0623949ae268)


# Document for terraform drift

|**Author**        | **created on**       | **Version** |**Last edited on**| **Review Level**   | **Reviewer**      |
|---------------|------------|---------|--------|--------|----------------------|
| Pravalika Kanikarapu  | Jun 18  | v1.0|   Jun 19  | Pre-Reviewer   | Priyanshu            |
| Pravalika Kanikarapu  |  |  |   | L0             | Priyanka     |
| Pravalika Kanikarapu  |      |      |         | L1             | Rishabh Sharma       |
| Pravalika Kanikarapu  |      |      |         | L2             | Piyush Upadhyay      |

# What is Terraform Drift?

Terraform drift refers to any difference between the infrastructure as deployed in the cloud and the infrastructure defined in Terraform configuration files (*.tf). Drift usually occurs due to:

- Manual changes in the cloud console

- Scripted changes outside Terraform

- Resource recreation by cloud services

# Why is Drift Detection Important?
- Prevents configuration mismatches.

- Maintains infrastructure as code (IaC) integrity.

- Detects manual or unauthorized changes.

- Enables early remediation before drift causes outages or security issues.

- Supports audits and compliance enforcement.


# Advantages 

| Advantage             | Explanation                                                          |
| --------------------- | -------------------------------------------------------------------- |
| Improved Security     | Detect unauthorized or insecure manual changes                       |
| Compliance Support    | Ensure actual infrastructure matches audited Terraform configuration |
| Reliable Rollbacks    | Avoid drift that breaks `terraform plan/apply` or rollback flows     |
| Visibility            | Get real-time awareness of infrastructure state                      |
| Cost Control          | Prevent untracked resources that incur costs                         |

# Best Practices

| **Best Practice**             | **Recommendation**                                                                 |
|------------------------------|-------------------------------------------------------------------------------------|
| **Remote State Management**  | Use remote backends like **S3** with **DynamoDB for state locking**.               |
| **State Consistency**        | **Never manually edit** the `.tfstate` file to avoid corruption or inconsistency.  |
| **Least Privilege IAM**      | Grant **read-only access** to drift detection tools for security.                  |
| **Alerting Integration**     | Integrate drift detection with **Slack**, **Email**, or **ticketing systems**.     |
| **Scheduled Automation**     | Run drift detection **daily or weekly**, depending on your infrastructure changes. |
| **Pre-Apply Checks**         | Always perform `terraform plan` before running `terraform apply`.                 |

# Drift Detection Strategy
The goal of drift detection is to identify and respond to any deviations between the actual deployed cloud infrastructure and the desired state defined in Terraform code.

## Approach

- **Compare States**  
  Use Terraform's internal `plan` mechanism to compare the current infrastructure state with the stored Terraform state.

- **External Scanning**  
  Leverage dedicated tools like **driftctl** to perform deep scans for unmanaged or drifted resources.

- **Automation Integration**  
  Integrate drift detection within **CI/CD pipelines** to ensure continuous monitoring without manual intervention.



## Notification and Remediation

- **Real-Time Alerts**  
  Notify teams immediately through **Slack** or **Email** upon detection of infrastructure drift.

- **Automated Response**  
  Optionally trigger **ticket creation** or **auto-remediation workflows** based on the **severity and criticality** of the drift.

# Automated Drift Detection

To ensure proactive and reliable drift detection, the following automation workflow will be implemented:


## Scheduled CI/CD Job

- A scheduled job (e.g., **daily at midnight**) will run as part of the CI/CD system (**Jenkins**, **GitHub Actions**, etc.).

---

## Drift Detection Commands

- Run `terraform plan -detailed-exitcode` to detect differences between the desired and actual infrastructure.
- Alternatively or additionally, execute `driftctl scan` for a deeper and more comprehensive analysis.

---

## Output Handling

- Parse CLI output to determine if drift has occurred:  
  - For `terraform plan`, **exit code 2** indicates drift.
- Generate **human-readable summaries** from the plan or scan output for clear reporting.

---

## Alerting

- If drift is detected, automatically send **notifications** to configured **Slack channels** or via **email**.

# Conclusion

Terraform drift detection is essential for infrastructure stability, security, and predictability. A proactive, automated strategy using tools like terraform plan, driftctl, and CI/CD integration ensures continuous alignment between code and real infrastructure state.


# Tools

| **Tool**                         | **Purpose**                                                                 |
|----------------------------------|-----------------------------------------------------------------------------|
| terraform plan                 | Native detection of drift using infrastructure comparison                  |
| driftctl                       | Enhanced detection of unmanaged and drifted resources                      |
| CI/CD Pipelines (e.g., Jenkins, GitHub Actions) | Automate detection as scheduled or event-driven jobs         |
| Slack / Email                    | Alerting mechanism to inform stakeholders of drift events                  |


#  Contact Information


| Name       | Email Address                |
|------------|------------------------------|
| Pravalika  | kanikarapu.pravalika.snaatak@mygurukulam.co|



#  Reference

| **Link**                                                                 | **Description**                                      |
|--------------------------------------------------------------------------|------------------------------------------------------|
| [TerraformDrift](https://spacelift.io/blog/terraform-drift-detection)| Documentation followed from this link .|



