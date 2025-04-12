# DevOps Training - Day 3

## Overview

Day 3 of the DevOps training was focused on enhancing our understanding of **AWS Identity and Access Management (IAM)** and deepening our practical knowledge of **EC2 instances**. The session provided both conceptual understanding and hands-on experience, leading up to setting up Docker and an introduction to CI/CD pipelines.

---

## AWS Identity and Access Management (IAM)

We began with a walkthrough of IAM services:

- Navigated to the **IAM** section in AWS Console.
- Created new users with:
  - Console access enabled.
  - Custom usernames and passwords.
  - Policies such as `AdministratorAccess` attached.
- Practiced logging in using a dedicated IAM sign-in URL with credentials.

This part focused on secure and structured access management within AWS environments.

---

## EC2 Instance Setup and SSH Access

We then revisited launching an EC2 instance:

- Used **Amazon Linux AMI** to create a virtual machine.
- Configured security groups and key pairs during launch.

### PuTTY SSH Access

- Downloaded and installed **PuTTY** and **PuTTYgen**.
- Converted `.pem` key to `.ppk` using PuTTYgen.
- Configured PuTTY:
  - **Host Name**: `ec2-user@<Public-IP>`
  - **SSH → Auth**: Loaded the `.ppk` key under Auth settings.

Once connected, we gained terminal access to the instance, enabling remote management.

---

## Installing Docker on EC2

Inside the EC2 terminal, we installed Docker for containerization:

### Commands Used:

```bash
sudo yum update -y
sudo yum install -y docker
sudo systemctl start docker
sudo systemctl enable docker
docker –version

