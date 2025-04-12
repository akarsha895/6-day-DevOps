# DevOps Training - Day 2: Hands-on with AWS Cloud Infrastructure

## Overview

On **Day 2** of the DevOps training program, we shifted from theoretical understanding to practical implementation by exploring **cloud infrastructure using Amazon Web Services (AWS)**. This hands-on session focused on setting up a personal AWS account, launching and configuring a virtual server, and gaining initial exposure to cloud-based environments.

---

## AWS Account Setup

The session began with guidance on creating an AWS account:
- Entered personal and contact details.
- Added debit card information for billing verification.
- Understood different AWS pricing models:
  - **Free Tier** – Ideal for beginners and limited testing.
  - **Pay-As-You-Go** – Flexible model that charges based on usage.

This setup is essential for accessing AWS services and performing cloud-based deployments in upcoming sessions.

---

## Launching an EC2 Instance

We proceeded to launch our first **EC2 (Elastic Compute Cloud)** instance using **Amazon Linux AMI**:

### Steps Followed:
1. **Selected EC2 Service** from the AWS Management Console.
2. **Chose an Amazon Machine Image (AMI)** – selected AWS Linux.
3. **Selected Instance Type** – e.g., `t2.micro` under Free Tier.
4. **Created a Key Pair** – downloaded `.pem` file for SSH access.
5. **Configured Security Group** – opened port 22 (SSH) for terminal access.
6. **Launched the Instance** – started the virtual server in the cloud.

---

## Accessing and Setting Up the Instance

After launching the EC2 instance, we accessed it using a terminal:

### Connecting via SSH:
```bash
ssh -i "my-key.pem" ec2-user@<public-ip-address>
Initial Setup Commands:
bash
CopyEdit
sudo yum update -y
We explored basic Linux commands and installed essential packages to prepare the environment for application deployment and configuration tasks in future sessions.
