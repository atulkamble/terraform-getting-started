# 🚀 Terraform Getting Started Practice  

A simple, structured Terraform project to practice infrastructure-as-code fundamentals: defining providers, creating AWS resources, handling variables, modules, outputs, state management, and useful commands.

---

## 📦 Project Directory Structure  

```bash
terraform-getting-started/
├── main.tf
├── providers.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
├── versions.tf
├── README.md
├── modules/
│   └── sample_module/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
└── .gitignore
````

---

## 📋 Requirements

* **Terraform v1.7+**
* **AWS CLI installed and configured** (`aws configure`)
* **AWS account credentials**

---

## 📄 Files Overview

### ✅ `versions.tf`

Specifies the required Terraform and AWS provider versions.

```hcl
terraform {
  required_version = ">= 1.7.0"

  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}
```

---

### ✅ `providers.tf`

Defines the AWS provider and region.

```hcl
provider "aws" {
  region = var.aws_region
}
```

---

### ✅ `variables.tf`

Declares input variables for region and EC2 instance name.

```hcl
variable "aws_region" {
  description = "AWS region to deploy resources"
  type        = string
  default     = "ap-south-1"
}

variable "instance_name" {
  description = "Name tag for EC2 instance"
  type        = string
  default     = "BasicTerraformInstance"
}
```

---

### ✅ `terraform.tfvars`

Provides values for declared variables.

```hcl
aws_region    = "ap-south-1"
instance_name = "MyTerraformInstance"
```

---

### ✅ `main.tf`

Creates an EC2 instance.

```hcl
resource "aws_instance" "web_server" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  tags = {
    Name = var.instance_name
  }
}
```

---

### ✅ `outputs.tf`

Defines outputs to display after `terraform apply`.

```hcl
output "instance_id" {
  description = "The ID of the EC2 instance"
  value       = aws_instance.web_server.id
}

output "public_ip" {
  description = "The public IP of the EC2 instance"
  value       = aws_instance.web_server.public_ip
}
```

---

### ✅ `modules/sample_module/`

A simple reusable module example to create an S3 bucket.

**`main.tf`**

```hcl
resource "aws_s3_bucket" "example_bucket" {
  bucket = var.bucket_name
  acl    = "private"
}
```

**`variables.tf`**

```hcl
variable "bucket_name" {
  description = "Name of the S3 bucket"
  type        = string
}
```

**`outputs.tf`**

```hcl
output "bucket_arn" {
  value = aws_s3_bucket.example_bucket.arn
}
```

---

### ✅ `.gitignore`

```gitignore
.terraform/
*.tfstate
*.tfstate.*
.crash
*.tfvars
*.tfvars.backup
*.backup
override.tf
override.tf.json
terraform.tfvars.json
```

---

## ⚙️ Terraform Workflow Commands

```bash
# Initialize Terraform working directory
terraform init  

# Validate syntax correctness
terraform validate  

# Format configuration files
terraform fmt -recursive  

# Show execution plan
terraform plan  

# Apply changes (with prompt)
terraform apply  

# Apply changes (auto-approve without prompt)
terraform apply -auto-approve  

# Destroy provisioned resources
terraform destroy  

# List resources in state
terraform state list  

# Show detailed state for a resource
terraform state show <resource_name>  

# Visualize resource dependency graph
terraform graph | dot -Tpng > graph.png  

# Import existing AWS resource into Terraform management
terraform import aws_instance.web_server i-0123456789abcdef0  

# View output values
terraform output  

# View a specific output value
terraform output instance_id  

# Check installed Terraform version
terraform version  

# Clean cached providers/plugins (use carefully)
terraform clean  

# Force unlock a stuck Terraform state
terraform force-unlock <LOCK_ID>
```

---

## 📌 Practice Exercises

✅ **Hands-on Tasks**

* [x] Deploy an EC2 instance
* [x] Output public IP, private IP, and instance ID
* [x] Create an S3 bucket using a module
* [x] Parameterize EC2 instance type with variables
* [x] Add variable validation (allowed instance types)
* [x] Use a data source to fetch latest Amazon Linux 2 AMI
* [x] Format, validate, and plan infrastructure
* [x] View state file and list managed resources
* [x] Import a manually-created S3 bucket
* [x] Generate and visualize dependency graph
* [x] Clean up infrastructure safely with `terraform destroy`

---

## 📚 Optional: Use a Data Source

Fetch latest Amazon Linux 2 AMI dynamically.

**In `main.tf`**

```hcl
data "aws_ami" "latest_amazon_linux" {
  most_recent = true

  owners = ["amazon"]

  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-*-x86_64-gp2"]
  }
}

resource "aws_instance" "web_server" {
  ami           = data.aws_ami.latest_amazon_linux.id
  instance_type = "t2.micro"

  tags = {
    Name = var.instance_name
  }
}
```

---

## 📝 Best Practices

* ✅ Always pin Terraform and provider versions (`versions.tf`)
* ✅ Regularly run `terraform fmt` to keep config consistent
* ✅ Validate configs before running `terraform plan`
* ✅ Modularize reusable infrastructure components
* ✅ Backup and protect state files (`terraform.tfstate`)
* ✅ Avoid hardcoding sensitive values — use variables or environment variables
* ✅ Use `terraform output` for post-deployment details
* ✅ Clean up resources properly to avoid charges

---

## 📚 Resources

* [Terraform Official Docs](https://developer.hashicorp.com/terraform/docs)
* [AWS Provider Docs](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)

---

## ✅ Author

Atul’s Terraform Practice

```

---
