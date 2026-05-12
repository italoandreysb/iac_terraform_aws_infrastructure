# IAC Terraform AWS Infrastructure

This project provisions AWS infrastructure using **Terraform**. It creates:

- A **VPC** (`10.0.0.0/16`) with an Internet Gateway
- A **public subnet** (`10.0.1.0/24`) with auto-assign public IP
- A **route table** with a default route to the Internet Gateway
- A **security group** allowing SSH (port 22) from anywhere (access only EC2 Key)
- An **EC2 instance** running Ubuntu 22.04 (configurable instance type, default `t3.micro`) in the public subnet
- An **output** with the EC2 public IP

**Required variable:** `key_name` (your EC2 key pair name).
**Optional variables:** `aws_region` (default `us-east-1`) and `instance_type` (default `t3.micro`).

## Prerequisites

- Terraform >= 1.5
- AWS credentials configured (`aws configure` or env vars)

### Install the AWS Key
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
rm -rf awscliv2.zip 
aws configure
```

Insira:

- Access Key (generate in AWS console)
- Secret Key
- região (sa-east-1)
- formato (json)


## Quick Start
1. In the AWS console, generate an Access Key and Secret Access Key using IAM.
2. In the AWS console, generate an EC2 Key Pair in the same region where the infrastructure will be deployed.
3. Run:

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
| `aws_region`   | `sa-east-1` | no       |
| `instance_type`| `t3.micro`  | no       |
| `key_name`     | —           | yes      |

## Clean Up

```bash
terraform destroy
```

