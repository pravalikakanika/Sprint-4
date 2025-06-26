

![image](https://github.com/user-attachments/assets/445e995f-5b72-4bcd-b44a-0623949ae268)

# Terraform Drift Detection - POC

|**Author**        | **created on**       | **Version** |**Last edited on**| **Review Level**   | **Reviewer**      |
|---------------|------------|---------|--------|--------|----------------------|
| Pravalika Kanikarapu  | Jun 27  | v1.0|   Jun 27  | Pre-Reviewer   | Priyanshu            |
| Pravalika Kanikarapu  |  |  |   | L0             | Priyanka     |
| Pravalika Kanikarapu  |      |      |         | L1             | Rishabh Sharma       |
| Pravalika Kanikarapu  |      |      |         | L2             | Piyush Upadhyay      |

# Objective

This Proof of Concept demonstrates how infrastructure **drift** can be detected using Terraform. Drift occurs when infrastructure is changed outside of Terraform’s control (e.g., via AWS Console or CLI), leading to a mismatch between the actual state and the Terraform state file.


