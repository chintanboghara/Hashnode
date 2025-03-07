---
title: "Terraform Associate: Customize Terraform Configuration with Variables"
seoTitle: "Customize Terraform with Variables"
seoDescription: "Customize Terraform using variables for dynamic, reusable infrastructure, enhancing flexibility and maintainability"
datePublished: Fri Mar 07 2025 03:30:37 GMT+0000 (Coordinated Universal Time)
cuid: cm7y7x3h600000ai9aigpg0sb
slug: terraform-associate-customize-terraform-configuration-with-variables
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1739926866600/f527d2b7-60a4-4ee0-98ba-bb1a08636092.png
tags: cloud, devops, sre, terraform, devsecops, platform-engineering, iac-infrastructure-as-code, terraform-associate

---

Terraform’s power lies in its flexibility. One of the key ways to make your infrastructure code more dynamic, reusable, and maintainable is by using **variables**. Instead of hardcoding values into your configuration files, you can define variables that accept different inputs during deployment. This approach allows you to tailor your infrastructure for different environments, simplify updates, and manage sensitive data more securely.

In this guide, we’ll explore:

* The types of Terraform variables.
    
* How to assign values using different methods.
    
* Output variables and sensitive variables.
    
* Best practices for working with variables.
    

## 1\. Types of Terraform Variables

Terraform supports several types of variables to help you customize your configurations dynamically.

### a) Input Variables

**Input variables** allow you to pass values into your Terraform configuration. They make your code more modular and adaptable.

#### Defining Input Variables

Create a file (e.g., `variables.tf`) and define your variables:

```plaintext
variable "aws_region" {
  description = "AWS region to deploy resources"
  type        = string
  default     = "us-west-2"
}
```

#### Using Variables in Your Configuration

Reference the variable in your main configuration file (e.g., `main.tf`):

```plaintext
provider "aws" {
  region = var.aws_region
}
```

### b) Environment Variables

Terraform can also assign variable values from environment variables that are prefixed with `TF_VAR_`.

#### Example

For a variable named `instance_type`, set it via the command line:

```bash
export TF_VAR_instance_type="t2.micro"
terraform apply
```

### c) Variable Types

Terraform supports various data types for variables:

| Type | Example |
| --- | --- |
| `string` | `"us-east-1"` |
| `number` | `2` |
| `bool` | `true` |
| `list` | `["t2.micro", "t3.micro"]` |
| `map` | `{ "dev": "t2.micro", "prod": "t3.large" }` |

#### List Variable Example

```plaintext
variable "instance_types" {
  type    = list(string)
  default = ["t2.micro", "t3.micro"]
}

resource "aws_instance" "example" {
  instance_type = var.instance_types[0]  # Uses "t2.micro"
}
```

#### Map Variable Example

```plaintext
variable "instance_type_map" {
  type    = map(string)
  default = {
    dev  = "t2.micro"
    prod = "t3.large"
  }
}

resource "aws_instance" "example" {
  instance_type = var.instance_type_map["dev"]
}
```

## 2\. Assigning Values to Variables

There are multiple ways to provide values for your variables:

### a) Command Line Flags

Pass variable values directly using the `-var` flag:

```bash
terraform apply -var="aws_region=us-east-1"
```

### b) Using a `.tfvars` File

Store your variable values in a `.tfvars` file (e.g., `terraform.tfvars`):

```plaintext
aws_region    = "us-east-1"
instance_type = "t2.medium"
```

Apply the configuration by referencing the file:

```bash
terraform apply -var-file="terraform.tfvars"
```

### c) Auto-Loaded Variable Files

Terraform automatically loads variables from files named:

* `terraform.tfvars`
    
* `*.auto.tfvars`
    

For example, if you create a file called `variables.auto.tfvars`:

```plaintext
aws_region = "us-east-1"
```

Terraform will load it automatically during execution—no need for extra flags.

## 3\. Output Variables

Output variables let you display or export values after your infrastructure has been applied. This is particularly useful for retrieving information such as IP addresses, resource IDs, or any computed values.

### Defining an Output Variable

In your configuration, add an output block:

```plaintext
output "instance_public_ip" {
  description = "Public IP of the EC2 instance"
  value       = aws_instance.example.public_ip
}
```

After running `terraform apply`, you can view the output:

```bash
terraform output instance_public_ip
```

## 4\. Sensitive Variables

For sensitive data (e.g., passwords or API keys), mark variables as **sensitive** to prevent their values from being displayed in logs or the CLI output.

### Marking a Variable as Sensitive

```plaintext
variable "db_password" {
  type      = string
  sensitive = true
}
```

When you run `terraform output`, the value will be hidden:

```bash
terraform output
# db_password = <sensitive>
```

## 5\. Best Practices for Terraform Variables

* **Avoid Hardcoding Values:** Use variables to make your configurations flexible and reusable.
    
* **Leverage** `.tfvars` Files: Maintain default variable values and manage configurations efficiently.
    
* **Mark Sensitive Data:** Use `sensitive = true` for secrets to avoid exposing them.
    
* **Use Maps and Lists:** Manage multiple environments or configurations more effectively with complex data types.
    

## Conclusion

Using variables in Terraform transforms your configurations into flexible, dynamic, and reusable code. By defining input variables, utilizing environment variables, and taking advantage of output and sensitive variables, you can tailor your infrastructure deployments to suit various environments and requirements.

Embrace these practices to create modular, secure, and maintainable Terraform configurations that scale with your infrastructure needs. Happy Terraforming!

## **Reference**

1. [Terraform Variables Documentation](https://www.terraform.io/language/values/variables)  
    *Explore how to define, use, and manage various types of variables in Terraform, including input, output, and sensitive variables.*
    
2. [Terraform Configuration Best Practices](https://www.terraform.io/docs/language/index.html)  
    *Learn best practices for creating modular, reusable, and maintainable Terraform configurations, with a focus on dynamic variable usage.*
    
3. [Using Environment Variables in Terraform](https://www.terraform.io/cli/config/environment-variables)  
    *Understand how Terraform leverages environment variables prefixed with TF\_VAR\_ to assign values to your configuration.*
    
4. [Managing .tfvars Files in Terraform](https://www.terraform.io/language/values/variables#variable-definitions-and-assignments)  
    \*A detailed guide on using .tfvars and *.auto.tfvars files to simplify variable assignments and streamline your deployments.*
    
5. [Advanced Terraform Variable Types and Structures](https://www.terraform.io/language/expressions/type-constraints)  
    *Discover how to work with complex variable types like lists and maps to manage configurations across multiple environments.*