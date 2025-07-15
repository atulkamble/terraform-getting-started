## 📦 terraform-getting-started
```
terraform-getting-started/
├── main.tf
├── providers.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
├── README.md
├── modules/
│   └── sample_module/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
└── .gitignore
```

---

## 📜 File Contents

### **providers.tf**

```hcl
provider "aws" {
  region = var.aws_region
}
```

---

### **variables.tf**

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

### **main.tf**

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

### **outputs.tf**

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

### **terraform.tfvars**

```hcl
aws_region    = "ap-south-1"
instance_name = "MyTerraformInstance"
```

---

### **modules/sample\_module/main.tf** *(example modular structure)*

```hcl
resource "aws_s3_bucket" "example_bucket" {
  bucket = var.bucket_name
  acl    = "private"
}
```

---

### **modules/sample\_module/variables.tf**

```hcl
variable "bucket_name" {
  description = "Name of the S3 bucket"
  type        = string
}
```

---

### **modules/sample\_module/outputs.tf**

```hcl
output "bucket_arn" {
  value = aws_s3_bucket.example_bucket.arn
}
```

---

### **.gitignore**

```gitignore
.terraform/
terraform.tfstate
terraform.tfstate.*
.crash
*.tfvars.backup
*.backup
```

---

## 📄 README.md

```markdown
# 🚀 Terraform Getting Started Practice  

## 📌 Overview  

A simple Terraform project to practice infrastructure-as-code basics: defining providers, creating AWS resources, handling variables, outputs, and using basic commands.

---

## 📦 Directory Structure  

```

terraform-getting-started/
├── main.tf
├── providers.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
├── modules/
│   └── sample\_module/
└── .gitignore

````

---

## 📋 Requirements  

- Terraform v1.7+
- AWS CLI installed and configured (`aws configure`)
- AWS account access  

---

## ⚙️ Commands  

```bash
# Initialize Terraform
terraform init  

# Validate configuration
terraform validate  

# Format configuration
terraform fmt  

# Show execution plan
terraform plan  

# Apply configuration
terraform apply  

# Destroy resources
terraform destroy  

# Show current state
terraform state list  
terraform state show <resource_name>
````

---

## 📌 Practice Exercises

* Create an EC2 instance
* Output public IP and instance ID
* Create an S3 bucket via module
* Use variables and tfvars
* Format and validate configs
* Manage Terraform state

---

## 📚 Resources

* [Terraform Docs](https://developer.hashicorp.com/terraform/docs)
* [AWS Provider Docs](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)

---

## ✅ Author

Atul’s Terraform Practice

````

---

## ✅ How to Use  

```bash
cd terraform-getting-started/
terraform init
terraform validate
terraform plan
terraform apply
````

**Confirm on prompt `yes` to create resources.**

---
