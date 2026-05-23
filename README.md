# terraform-aws-networking-lab

# AWS Terraform Bastion Lab

## Project Overview

This project demonstrates the provisioning of a complete AWS networking and compute environment using Terraform.

The objective was to gain hands-on experience with:

- AWS networking fundamentals
- Infrastructure as Code (IaC)
- Terraform workflows
- EC2 provisioning
- Linux server management
- Security groups and routing
- Infrastructure lifecycle management

This was built entirely from scratch using AWS Free Tier resources.

---

# Architecture

```text
Internet
    │
Internet Gateway
    │
Route Table
    │
Public Subnet (10.0.1.0/24)
    │
EC2 Bastion Host (Ubuntu + NGINX)
    │
VPC (10.0.0.0/16)
```

---

# Technologies Used

- AWS
- Terraform
- EC2
- VPC
- Internet Gateway
- Route Tables
- Security Groups
- Ubuntu Linux
- NGINX
- SSH
- AWS CLI

---

# Infrastructure Components

## VPC
Created a custom VPC with CIDR:

```hcl
10.0.0.0/16
```

Features enabled:
- DNS hostnames
- DNS resolution

---

## Public Subnet

Created a public subnet:

```hcl
10.0.1.0/24
```

Availability Zone:
```text
ap-south-1a
```

Configured:
- automatic public IP assignment

---

## Internet Gateway

Provisioned and attached an Internet Gateway to enable internet access for resources inside the VPC.

---

## Route Table

Configured a public route:

```hcl
0.0.0.0/0 → Internet Gateway
```

Associated the route table with the public subnet.

---

## Security Group

Created a security group allowing:

### SSH
```text
TCP 22
```

### HTTP
```text
TCP 80
```

Ingress temporarily allowed from:
```text
0.0.0.0/0
```

---

## EC2 Bastion Host

Provisioned:
- Ubuntu EC2 instance
- Public IP enabled
- SSH key authentication

Connected successfully using SSH.

---

# Terraform Workflow

## Initialize Terraform

```bash
terraform init
```

## Review Execution Plan

```bash
terraform plan
```

## Apply Infrastructure

```bash
terraform apply
```

## View Terraform State

```bash
terraform state list
```

## Destroy Infrastructure

```bash
terraform destroy
```

---

# Linux Commands Used

## Verify User

```bash
whoami
```

## Check Hostname

```bash
hostname
```

## Check Network Interfaces

```bash
ip a
```

## Check Disk Usage

```bash
df -h
```

## Check Memory Usage

```bash
free -m
```

## Verify NGINX

```bash
systemctl status nginx
```

## Check Running Processes

```bash
ps aux | grep nginx
```

## Check Listening Ports

```bash
sudo netstat -tulpn | grep 80
```

---

# Packages Installed

```bash
sudo apt update && sudo apt install -y nginx htop net-tools curl unzip
```

Installed:
- nginx
- htop
- net-tools
- curl
- unzip

---

# Key Learnings

## AWS Networking

Learned:
- VPC design
- subnetting
- public routing
- internet gateways
- security groups

---

## Terraform Concepts

Learned:
- Infrastructure as Code
- dependency graph
- Terraform state
- idempotency
- infrastructure lifecycle management

---

## Linux Administration

Learned:
- service management
- process inspection
- network troubleshooting
- package installation

---

## Cloud Engineering Principles

Learned:
- infrastructure provisioning
- infrastructure teardown
- debugging deployment issues
- public vs private networking
- SSH authentication

---

# Challenges Faced

## Region Visibility Issue

Initially resources were not visible because AWS Console region differed from Terraform provider region.

Resolved by switching AWS Console region to:
```text
ap-south-1 (Mumbai)
```

---

## EC2 Free Tier Error

Encountered:

```text
InvalidParameterCombination:
The specified instance type is not eligible for Free Tier
```

Resolved by changing:

```hcl
t2.micro → t3.micro
```

---

# Final Outcome

Successfully:
- provisioned AWS infrastructure using Terraform
- deployed Ubuntu EC2 instance
- connected using SSH
- installed and verified NGINX
- validated networking and routing
- managed infrastructure lifecycle using Terraform

---

# Future Improvements

Planned next steps:
- private subnets
- NAT Gateway
- IAM roles
- S3 backend for Terraform state
- remote state locking
- CI/CD integration
- Docker deployment
- Kubernetes (EKS)
- monitoring and observability

---

# Cleanup Verification

All infrastructure resources were destroyed using:

```bash
terraform destroy
```

Verified cleanup in AWS Console to avoid orphan resources and unnecessary billing.
