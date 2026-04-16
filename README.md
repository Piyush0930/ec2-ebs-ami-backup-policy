# EC2 EBS-Backed AMI Backup Policy (AWS DLM)

## Overview
This repository documents the AWS Data Lifecycle Manager (DLM) policy used to automatically create AMI backups for an EC2 instance.

---

## Instance Details
- Instance ID: i-0c7fe067e904447fa
- Region: eu-west-2 (London)
- Instance Type: t3.micro
- OS: Ubuntu 24.04 LTS

---

## Backup Policy Details

### Policy Type
- EBS-backed AMI Policy (AWS DLM)

### Schedule
- Frequency: Every 1 hour
- Start Time: 06:35 UTC

### Retention
- Maximum AMIs retained: 3
- Oldest AMI age: ≤ 3 hours

---

## Target Selection
The policy targets instances with the following tag:

- Key: Backup  
- Value: Yes  

---

## What This Policy Does

When triggered, AWS DLM automatically:

1. Creates an AMI of the EC2 instance
2. Creates EBS snapshots for all attached volumes
3. Associates snapshots with the AMI
4. Deletes older AMIs based on retention rules

---

## Important Notes

- AMIs can be used to launch new EC2 instances
- Snapshots are managed automatically by AWS DLM
- No manual backup is required once policy is active
- Instance must always have correct tag (`Backup=Yes`)

---

## Restore Process

To restore the server:

1. Go to AWS EC2 Console
2. Open AMIs section
3. Select latest AMI
4. Click "Launch Instance"

This creates a new EC2 instance with same configuration and data.

---

## Purpose

This setup ensures:
- Automated backup every 1 hour
- Fast recovery in case of failure
- Minimal manual intervention
