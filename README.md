# IAC Terraform AWS Infrastructure

This project provisions AWS infrastructure using **Terraform**. It creates:

- A **VPC** (`10.0.0.0/16`) with an Internet Gateway
- A **public subnet** (`10.0.1.0/24`) with auto-assign public IP
- A **route table** with a default route to the Internet Gateway
- A **security group** allowing SSH (port 22) from anywhere
- An **EC2 instance** running Ubuntu 22.04 (configurable instance type, default `t3.micro`) in the public subnet
- An **output** with the EC2 public IP

**Required variable:** `key_name` (your EC2 key pair name).
**Optional variables:** `aws_region` (default `us-east-1`) and `instance_type` (default `t3.micro`).

## Prerequisites

## Prerequisites

- Terraform >= 1.5
- AWS credentials configured (`aws configure` or env vars)

## Quick Start

```bash
cp .env_example .env
source .env
terraform init
terraform plan
terraform apply
```

## Variables

Set via `.env` (using `TF_VAR_` prefix) or `terraform.tfvars`:

| Variable        | Default     | Required |
|----------------|-------------|----------|
| `aws_region`   | `us-east-1` | no       |
| `instance_type`| `t3.micro`  | no       |
| `key_name`     | —           | yes      |

## Clean Up

```bash
terraform destroy
```
