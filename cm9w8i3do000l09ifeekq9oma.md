---
title: "Terraform Associate: Build and Use a Local Module"
seoTitle: "Create and Use Terraform Local Modules"
seoDescription: "Build Terraform local modules to organize code, enhance reusability, and simplify infrastructure management for efficient deployments"
datePublished: Fri Apr 25 2025 03:30:49 GMT+0000 (Coordinated Universal Time)
cuid: cm9w8i3do000l09ifeekq9oma
slug: terraform-associate-build-and-use-a-local-module
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1743747274862/8ee6cf3a-58a9-460c-bb7c-36de30c88dee.png
tags: cloud, devops, sre, terraform, devsecops, platform-engineering, iac-infrastructure-as-code, terraform-associate

---

Terraform local modules are a powerful feature that helps you organize your code, promote reusability, and simplify infrastructure management. By encapsulating common infrastructure patterns into modules, you can build a module once and use it multiple times across different projects, reducing redundancy and improving maintainability.

## Why Use a Local Module?

Local modules offer several significant benefits:

* **Encapsulation:** Bundle related resources, such as VPCs, EC2 instances, and IAM roles, into a single, coherent module.
    
* **Reusability:** Write your configuration once and reuse it across multiple projects, ensuring consistency.
    
* **Readability & Maintainability:** Break complex configurations into manageable pieces, making the code easier to understand and update.
    
* **Modular Updates:** Update a module in one place without the need to modify every instance of its usage in your main configuration.
    

## Creating a Local Module

A Terraform module is simply a directory that contains one or more `.tf` files. Organizing your modules in a dedicated folder structure not only keeps your project tidy but also makes your configuration more scalable.

### Folder Structure Example

```plaintext
terraform-project/
│── main.tf         # Calls the module
│── modules/
│   └── ec2-instance/
│       ├── main.tf        # Defines the resources (e.g., EC2 instance)
│       ├── variables.tf   # Defines input variables
│       └── outputs.tf     # Defines output values
│   └── vpc/         # (Optional) Another module for VPC configuration
│       └── main.tf
```

## Writing a Local Module

Let’s walk through the process of creating a local module that provisions an EC2 instance.

### Step 1: Define the Module (`modules/ec2-instance/main.tf`)

This file contains the resource definitions. For example, to create an AWS EC2 instance:

```plaintext
resource "aws_instance" "web" {
  ami           = var.ami
  instance_type = var.instance_type

  tags = {
    Name = var.instance_name
  }
}
```

### Step 2: Define Input Variables (`modules/ec2-instance/variables.tf`)

Input variables allow you to parameterize the module. Here, you define the variables for the AMI, instance type, and instance name:

```plaintext
variable "ami" {
  description = "The AMI ID for the EC2 instance"
  type        = string
}

variable "instance_type" {
  description = "The instance type"
  type        = string
  default     = "t3.micro"
}

variable "instance_name" {
  description = "The name tag for the instance"
  type        = string
}
```

### Step 3: Define Output Variables (`modules/ec2-instance/outputs.tf`)

Outputs allow you to expose key attributes of the resources created by the module, such as the instance ID and public IP address:

```plaintext
output "instance_id" {
  description = "The ID of the EC2 instance"
  value       = aws_instance.web.id
}

output "public_ip" {
  description = "The public IP of the EC2 instance"
  value       = aws_instance.web.public_ip
}
```

## Using the Local Module in Your Main Configuration

Once your module is defined, you can call it from your main Terraform configuration file. This makes it easy to integrate and reuse the module across your project.

### Example Usage (`main.tf`)

```plaintext
module "ec2_instance" {
  source         = "./modules/ec2-instance"
  ami            = "ami-12345678"
  instance_type  = "t3.micro"
  instance_name  = "MyWebServer"
}
```

After deploying the module, you can access its outputs and use them elsewhere in your configuration. For instance:

```plaintext
output "ec2_public_ip" {
  value = module.ec2_instance.public_ip
}
```

## Initializing and Applying the Configuration

To deploy the infrastructure defined in your Terraform configuration, use the following commands:

1. **Initialize Terraform:**
    
    This command downloads the necessary providers and modules.
    
    ```sh
    terraform init
    ```
    
2. **Apply the Configuration:**
    
    This command creates the resources defined in your configuration.
    
    ```sh
    terraform apply
    ```
    

After a successful deployment, Terraform will display the outputs defined in your module, such as the EC2 instance ID and its public IP address.

## Best Practices for Local Modules

To ensure that your modules are effective and maintainable, consider the following best practices:

1. **Keep Modules Focused:** Design each module to handle a single responsibility. This makes them easier to understand and reuse.
    
2. **Use Meaningful Names:** Clearly define variables and outputs with descriptive names and documentation to facilitate collaboration.
    
3. **Organize Your Code:** Store modules in a dedicated `modules/` directory within your project.
    
4. **Avoid Hardcoding:** Use variables to allow for flexibility and adaptability across different environments.
    
5. **Document Your Modules:** Include comments or documentation to describe the purpose, inputs, outputs, and any dependencies of your modules.
    

## Conclusion

Local modules in Terraform are a powerful tool for managing infrastructure as code. By encapsulating common configurations into reusable modules, you can improve code organization, enhance maintainability, and speed up your deployment process. Whether you're provisioning a single EC2 instance or orchestrating a complex multi-component architecture, using local modules helps ensure consistency and scalability across your projects.

Embrace the modular approach in Terraform to build robust, efficient, and maintainable infrastructure with ease. Happy coding!

## Reference

1. [Terraform Modules Documentation](https://developer.hashicorp.com/terraform/language/modules)  
    This official documentation provides comprehensive insights into how Terraform modules work, including guidance on creating and managing local modules.
    
2. [Terraform: Modules - Getting Started](https://learn.hashicorp.com/tutorials/terraform/module)  
    A beginner-friendly tutorial that walks you through the process of developing and using Terraform modules, ideal for understanding local module creation and best practices.
    
3. [DigitalOcean Tutorial: How to Use Terraform Modules](https://www.digitalocean.com/community/tutorials/how-to-use-terraform-modules)  
    This step-by-step guide explains the benefits and implementation of Terraform modules, highlighting how local modules can simplify infrastructure management.
    
4. [Gruntwork: Best Practices for Terraform Modules](https://www.gruntwork.io/guides/terraform/best-practices-for-terraform-modules)  
    An in-depth resource on structuring and optimizing your Terraform modules, offering valuable tips for improving code reusability and maintainability.
    
5. [HashiCorp Blog: Organizing Infrastructure Code with Modules](https://www.hashicorp.com/resources/terraform-best-practices)  
    Explore best practices and real-world examples of how to organize and manage your infrastructure code using modules, ensuring efficient and scalable deployments.