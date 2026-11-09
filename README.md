# Automated AWS Infrastructure with Terraform

Provisions a complete AWS environment as code: a VPC with public and private
subnets, an EC2 web server, an RDS database and an S3 bucket serving a static
website — deployed through a GitHub Actions pipeline.

This is a learning project built to practise Infrastructure as Code end to end.
It runs as a temporary test environment: the pipeline tears the infrastructure
down again after every deployment so nothing is left running in the account.

## Architecture

The configuration is split into four modules:

| Module | Purpose |
| --- | --- |
| `modules/networking` | VPC, public and private subnets, internet gateway, route tables |
| `modules/compute` | EC2 instance and security groups for the web server |
| `modules/rds` | RDS instance in a private subnet |
| `modules/s3` | S3 bucket configured for static website hosting |

`main.tf` wires the modules together, `variables.tf` declares the inputs and
`outputs.tf` exposes the endpoints. `graph.png` and `terraform-graph.png` show
the resource dependency graph.

## Prerequisites

- AWS CLI, configured with credentials
- Terraform 1.7 or later
- An AWS account (Free Tier is sufficient)

## Quick start

```bash
git clone https://github.com/sodbilegtb/AWS_IaC_Terraform.git
cd AWS_IaC_Terraform

# Variables: copy the example and fill in your own values
cp terraform.tfvars.example terraform.tfvars

# The database password is never stored in a file
export TF_VAR_db_password='your-password'

terraform init
terraform plan
terraform apply
terraform output
```

Tear everything down again when you are done:

```bash
terraform destroy
```

## Configuration

`terraform.tfvars` is excluded via `.gitignore` and must not be committed —
it holds account-specific values. Use `terraform.tfvars.example` as the
template. `db_password` is declared `sensitive` and is passed through the
`TF_VAR_db_password` environment variable rather than any file.

## S3 static website hosting

Terraform creates an S3 bucket with website hosting enabled and a bucket policy
that makes the content in `src/` publicly readable. The website URL is part of
the Terraform outputs.

## CI/CD with GitHub Actions

The workflow lives in `.github/workflows/deploy.yml` and runs on every push to
`main` and on pull requests:

1. TFLint
2. `terraform init` and `terraform validate`
3. `terraform plan`
4. `terraform apply` — only on pushes to `main`
5. `terraform destroy` — tears the test environment down again

The following repository secrets are required:

| Secret | Purpose |
| --- | --- |
| `AWS_ACCESS_KEY_ID` | AWS credentials for the pipeline |
| `AWS_SECRET_ACCESS_KEY` | AWS credentials for the pipeline |
| `TF_VAR_DB_PASSWORD` | Password for the RDS instance |
| `TF_VAR_BUCKET_NAME` | Globally unique name for the S3 bucket |

## Possible next steps

- Auto Scaling group and Application Load Balancer for high availability
- Dedicated IAM roles instead of static access keys (OIDC)
- Remote state in S3 with DynamoDB state locking
