# AWS Cloud IAM – Least Privilege Implementation

![AWS IAM](https://img.shields.io/badge/AWS-IAM-FF9900?style=flat-square&logo=amazonaws&logoColor=white)
![Status](https://img.shields.io/badge/status-complete-brightgreen?style=flat-square)
![Security](https://img.shields.io/badge/security-least%20privilege-blue?style=flat-square)

A hands-on implementation of the Principle of Least Privilege (PoLP) for a simulated company, TechCorp Enterprises, using AWS IAM. Each user was given exactly the permissions their role requires — nothing more.

---

## Overview

Rather than assigning permissions broadly, this project models how a real company should structure IAM from the start. Permissions live on groups, users inherit from groups, and every access decision is intentional.

---

## Architecture

| Type | Identity | Policy | Purpose |
|------|----------|--------|---------|
| Group | Engineering-Group | AmazonEC2FullAccess | Manage EC2 instances |
| Group | Finance-Group | AWSBillingReadOnlyAccess | View billing only |
| User | Manny | via Engineering-Group | Simulated Developer |
| User | Mike | via Finance-Group | Simulated Accountant |

---

## Security Measures

- MFA enforced on the root account.
- Root account is not used for any day-to-day operations.
- All permissions are assigned at the group level, not to individual users.
- No inactive users were left enabled.

---

## Test Results

**Manny (Developer)**

| Resource | Result |
|----------|--------|
| EC2 Access | Success |
| Billing Access | Denied |

**Mike (Accountant)**

| Resource | Result |
|----------|--------|
| Billing Access | Success |
| EC2 Access | Denied |
| S3 Access | Denied |

---

## Screenshots

*Add Access Denied screenshots here.*

---

## Key Takeaways

- Group-based permissions scale well. Adding a new developer means one group assignment, not a manual policy review.
- Least privilege limits the blast radius of a compromised account. Manny can't touch billing; Mike can't touch infrastructure.
- MFA on root is the most important single control in an AWS account.
- Attaching policies to users directly is a maintenance problem waiting to happen.
