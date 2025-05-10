---
title: "Terraform Associate: Module Creation - Recommended Pattern"
seoTitle: "Best Practices for Creating Terraform Modules"
seoDescription: "Learn to create efficient Terraform modules with a recommended structure for consistency, versioning, testing, CI/CD, and security practices"
datePublished: Sat May 10 2025 03:30:19 GMT+0000 (Coordinated Universal Time)
cuid: cmaho38aj000p09l88nfu8g6o
slug: terraform-associate-module-creation-recommended-pattern
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1745986168332/e7756392-fefa-40cb-afdd-3d52d0190355.png
tags: cloud, devops, sre, terraform, devsecops, platform-engineering, iac-infrastructure-as-code, terraform-associate

---

Infrastructure as code (IaC) empowers teams to provision, manage, and version their cloud resources just like application code. But as your Terraform codebase grows, so does the risk of duplication, drift, and configuration sprawl. Enter **Terraform modules,** the building blocks that let you encapsulate, share, and reuse infrastructure patterns safely and consistently. In this post, we’ll walk through a recommended module structure, best practices to keep your modules clean and consumable, and a few extra tips around testing, CI/CD, and security.

### Why Modules Matter

* **DRY Principle**: Avoid copy-pasting VPCs, subnets, or IAM roles across environments.
    
* **Consistency**: Enforce a single configuration source, and everyone uses the same defaults, tags, and security posture.
    
* **Versioning & Distribution**: Lock to semantic versions or share via the Terraform Registry.
    
* **Onboarding & Documentation**: Self-documented modules with examples make it easy for new team members to deploy infrastructure correctly.
    

## 1\. General Module Structure

Start each module with a consistent directory layout:

```markdown
my-module/
├── main.tf         # Core resource definitions
├── variables.tf    # Input variable declarations
├── outputs.tf      # Output variables for downstream consumption
├── README.md       # Usage instructions, variable/output tables, caveats
└── examples/       # Concrete example configurations
    └── simple/     # e.g., examples/simple/main.tf
```

This structure immediately tells users where to look for logic (`main.tf`), knobs (`variables.tf`), and documentation (`README.md`).

## 2\. Core Files Explained

### a) `main.tf` – The Module Logic

Here you define the AWS, GCP, Azure, or other resources your module provisions. Keep resources tightly scoped to one responsibility.

```markdown
resource "aws_instance" "this" {
  ami           = var.ami_id
  instance_type = var.instance_type
  tags = {
    Name        = var.instance_name
    Environment = var.environment
  }
}
```

> **Tip:** Use the `this` convention for your primary resource to avoid collisions when multiple resources live in one file.

### b) `variables.tf` – Inputs & Validation

Expose every configurable aspect as a variable, with helpful descriptions, type constraints, and defaults.

```markdown
variable "ami_id" {
  description = "The AMI ID for launching the EC2 instance"
  type        = string
}

variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t3.micro"

  validation {
    condition     = contains(["t3.micro", "t3.small", "t3.medium"], var.instance_type)
    error_message = "Allowed types: t3.micro, t3.small, t3.medium."
  }
}

variable "instance_name" {
  description = "Name tag for the instance"
  type        = string
}

variable "environment" {
  description = "Deployment environment (e.g., dev, staging, prod)"
  type        = string
  default     = "dev"
}
```

> **Tip:** Leverage `validation` blocks to catch misconfigurations early, and set defaults for “safe” values whenever possible.

### c) `outputs.tf` – What You’ll Need Downstream

Outputs let parent modules or root configurations consume IDs, endpoints, and other dynamic values.

```markdown
output "instance_id" {
  description = "The AWS EC2 instance ID"
  value       = aws_instance.this.id
}

output "public_ip" {
  description = "The public IP address"
  value       = aws_instance.this.public_ip
}
```

> **Best Practice:** Name outputs clearly and include descriptions so they auto-populate in tooling like `terraform-docs` or in CI logs.

### d) `README.md` – Your Module’s Front Door

Write a concise yet comprehensive README covering:

1. **Purpose**
    
2. **Usage Example**
    
3. **Inputs & Defaults** (table)
    
4. **Outputs** (table)
    
5. **Dependencies** (e.g., provider requirements)
    
6. **Caveats & Permissions** (e.g., “requires AWS credentials with `ec2:DescribeInstances`”)
    

````markdown
# EC2 Instance Module

Creates a single EC2 instance with customizable AMI, instance type, and tags.

## Usage

```hcl
module "web_server" {
  source         = "git::https://github.com/acme/terraform-modules.git//ec2-instance?ref=v1.2.0"
  ami_id         = "ami-0abc12345def67890"
  instance_type  = "t3.small"
  instance_name  = "frontend-01"
  environment    = "prod"
}
````

| Variable | Description | Type | Default |
| --- | --- | --- | --- |
| `ami_id` | AMI ID for the EC2 instance | string | n/a |
| `instance_type` | EC2 instance type (`t3.micro`, `t3.small`) | string | `t3.micro` |
| `environment` | Deployment environment | string | `dev` |

| Output | Description |
| --- | --- |
| `instance_id` | The ID of the created EC2 instance |
| `public_ip` | The public IP address for the instance |

> **Tooling:** Automate your README generation with terraform-docs.

### e) `examples/` – Show, Don’t Just Tell

Under `examples/`, include one or more folders, each with a minimal `main.tf` that pulls in your module and outputs key values. This accelerates discovery and lowers the bar for adoption.

## 3\. Advanced Best Practices

1. **One Responsibility per Module**
    
    * Keep modules focused: VPC here, EC2 there, RDS elsewhere.
        
2. **Version Control & Semantic Versioning**
    
    * Tag releases (v1.0.0) and reference them (`?ref=v1.0.0`) to prevent drift.
        
3. **Automated Testing**
    
    * Use Terratest or Kitchen-Terraform to spin up resources in a sandbox and verify outputs.
        
4. **CI/CD Integration**
    
    * Lint with `tflint`, `checkov` for security scanning, and `terraform fmt`/`validate` in your pipeline.
        
5. **Security Hygiene**
    
    * Scan your HCL for hard-coded secrets and enforce least-privilege IAM roles via variable inputs.
        
6. **Documentation Portals**
    
    * If you publish internally, consider a docs site (MkDocs, GitBook) that pulls in your module README’s automatically.
        
7. **Lifecycle Management**
    
    * Where appropriate, use `lifecycle { prevent_destroy = true }` to protect critical resources.
        
8. **Naming & Tagging Standards**
    
    * Enforce corporate naming conventions via variables and automated validation blocks.
        

## 4\. Putting It All Together: A VPC Module Example

Imagine a `vpc-module/` with:

* `main.tf`: Defines VPC, public and private subnets, route tables.
    
* `variables.tf`: Exposes CIDR blocks, AZ list, tags, and optional NAT gateway count.
    
* `outputs.tf`: Returns `vpc_id`, `public_subnet_ids`, `private_subnet_ids`.
    
* `README.md`: Shows how to reference the module, variable table, outputs table, and notes on Internet Gateway permissions.
    
* `examples/complete/`: Demonstrates a multi-AZ usage with NAT Gateways.
    

By following this pattern, you get:

* **Discoverable Documentation**
    
* **Automated Validation & Security**
    
* **Test-Driven Reliability**
    
* **Reusable Versioned Code**
    

## Final Thoughts

Building Terraform modules is both an art and a discipline—it’s about striking the right balance between flexibility and guardrails. With a clear folder structure, well-defined inputs/outputs, comprehensive documentation, and a robust testing/CI pipeline, your modules become true building blocks rather than one-off scripts.

Start small, iterate often, and invest in automation early. Over time, you’ll find your team moving faster, making fewer mistakes, and building a sturdy, shareable foundation for all your cloud infrastructure. Happy modularizing!

## Reference

1. [Terraform Modules: Developing](https://developer.hashicorp.com/terraform/language/modules/develop)  
    Official HashiCorp documentation on module structure, inputs/outputs, and development workflows.
    
2. [HashiCorp Blog: Terraform Module Best Practices](https://www.hashicorp.com/resources/terraform-best-practices)  
    Guidance on applying the DRY principle, versioning, and module distribution strategies.
    
3. [Gruntwork: Terraform Testing with Terratest](https://gruntwork.io/guides/terraform/testing-terraform-with-terratest/)  
    A hands-on tutorial for writing automated tests that validate your modules using Go and Terratest.
    
4. [tfsec & Checkov: Infrastructure as Code Security Scanning](https://www.checkov.io/)  
    Tools and techniques for statically analyzing Terraform code to detect security, compliance, and configuration issues.
    
5. [Terraform-docs: Automate README Generation](https://github.com/terraform-docs/terraform-docs)  
    A CLI tool to generate living documentation (inputs/outputs tables) from your module’s code and keep README.md in sync.