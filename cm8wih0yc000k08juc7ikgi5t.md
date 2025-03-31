---
title: "Terraform Associate: Create Dynamic Expressions"
seoTitle: "Dynamic Expressions in Terraform Explained"
seoDescription: "Use dynamic expressions in Terraform to enhance infrastructure flexibility via variables, loops, and conditionals for scalable deployments"
datePublished: Mon Mar 31 2025 03:30:13 GMT+0000 (Coordinated Universal Time)
cuid: cm8wih0yc000k08juc7ikgi5t
slug: terraform-associate-create-dynamic-expressions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1741326100344/784fdb74-61db-4a25-b32a-0f15ec669e31.png
tags: cloud, devops, sre, terraform, devsecops, platform-engineering, iac-infrastructure-as-code, terraform-associate

---

Terraform’s power goes beyond merely defining static resources—its dynamic expressions empower you to build flexible, scalable, and maintainable infrastructure as code. By leveraging variables, functions, conditionals, loops, and lookups, you can generate dynamic values for your resources, streamlining your configurations and reducing the need for repetitive hardcoding.

In this guide, we’ll explore various dynamic expression techniques in Terraform with practical examples and best practices to help you create adaptable and efficient infrastructure configurations.

## 1\. Using Variables in Expressions

Input variables allow you to inject dynamic values into your resources. For instance, you can conditionally set an EC2 instance type based on the environment.

### Example: Dynamic EC2 Instance Type Based on Environment

```plaintext
variable "environment" {
  type    = string
  default = "dev"
}

resource "aws_instance" "web" {
  ami           = "ami-12345678"
  instance_type = var.environment == "prod" ? "t3.large" : "t3.micro"
}
```

* **Explanation:**  
    If the `environment` is set to `"prod"`, Terraform uses a larger instance type (`t3.large`); otherwise, it defaults to a smaller type (`t3.micro`). This simple conditional makes it easy to adapt resources based on deployment context.
    

## 2\. Conditional Expressions (`? :`)

Conditional expressions provide if-else logic within your configuration, allowing you to dynamically assign values based on conditions.

### Example: Assigning Storage Size Based on Environment

```plaintext
variable "env" {
  default = "dev"
}

resource "aws_instance" "server" {
  ami           = "ami-12345678"
  instance_type = "t3.micro"
  
  root_block_device {
    volume_size = var.env == "prod" ? 100 : 50
  }
}
```

* **Explanation:**  
    Here, the root block device's volume size is set to 100GB for a production environment and 50GB for development, ensuring that resources are appropriately sized for different environments.
    

## 3\. Using `for_each` for Dynamic Resource Creation

The `for_each` loop allows you to create multiple resources dynamically based on a collection of values.

### Example: Create Multiple S3 Buckets

```plaintext
variable "bucket_names" {
  type    = list(string)
  default = ["bucket1", "bucket2", "bucket3"]
}

resource "aws_s3_bucket" "example" {
  for_each = toset(var.bucket_names)

  bucket = each.value
}
```

* **Explanation:**  
    With `for_each`, Terraform iterates over the list of bucket names and creates an S3 bucket for each item. This approach is ideal when you need to manage a variable number of similar resources.
    

## 4\. Using `count` for Dynamic Scaling

When you need to create several instances of the same resource, the `count` parameter can be used for dynamic scaling.

### Example: Create Multiple EC2 Instances

```plaintext
variable "instance_count" {
  default = 3
}

resource "aws_instance" "web" {
  count         = var.instance_count
  ami           = "ami-12345678"
  instance_type = "t3.micro"
}
```

* **Explanation:**  
    The `count` parameter instructs Terraform to create three EC2 instances when `instance_count` is set to 3, simplifying the process of scaling out your infrastructure.
    

## 5\. Dynamic Block Configuration with `for_each`

For resources with nested blocks that require dynamic configuration, the `dynamic` block allows you to iterate over collections to generate nested blocks.

### Example: Dynamic Security Group Rules

```plaintext
variable "ingress_rules" {
  type = list(object({
    port        = number
    cidr_blocks = list(string)
  }))
  default = [
    { port = 80, cidr_blocks = ["0.0.0.0/0"] },
    { port = 443, cidr_blocks = ["0.0.0.0/0"] }
  ]
}

resource "aws_security_group" "web" {
  name = "web-sg"

  dynamic "ingress" {
    for_each = var.ingress_rules

    content {
      from_port   = ingress.value.port
      to_port     = ingress.value.port
      protocol    = "tcp"
      cidr_blocks = ingress.value.cidr_blocks
    }
  }
}
```

* **Explanation:**  
    This configuration dynamically creates multiple ingress rules for the security group based on the provided list. It’s an efficient way to manage nested configurations that vary in quantity or content.
    

## 6\. Using `lookup()` for Dynamic Map Values

The `lookup()` function retrieves values from a map dynamically, providing a default value if the key does not exist.

### Example: Select an AMI Based on Region

```plaintext
variable "region" {
  default = "us-east-1"
}

variable "ami_map" {
  default = {
    "us-east-1" = "ami-12345678"
    "us-west-2" = "ami-87654321"
  }
}

resource "aws_instance" "web" {
  ami           = lookup(var.ami_map, var.region, "ami-default")
  instance_type = "t3.micro"
}
```

* **Explanation:**  
    The `lookup()` function checks `var.ami_map` for the key corresponding to the region. If found, it returns the associated AMI; otherwise, it defaults to `"ami-default"`. This is particularly useful for multi-region deployments.
    

## 7\. Combining Expressions for Advanced Logic

You can combine multiple expressions to implement more sophisticated decision-making logic.

### Example: Select a Value Based on Multiple Conditions

```plaintext
variable "env" {
  default = "dev"
}

variable "instance_map" {
  default = {
    "dev"  = "t3.micro"
    "test" = "t3.medium"
    "prod" = "t3.large"
  }
}

resource "aws_instance" "server" {
  instance_type = lookup(var.instance_map, var.env, "t2.micro")
}
```

* **Explanation:**  
    This example combines a variable and a lookup function to choose an appropriate EC2 instance type based on the environment. If the environment isn’t defined in the map, it defaults to `"t2.micro"`.
    

## 8\. Best Practices for Dynamic Expressions

To maximize the benefits of dynamic expressions in Terraform, consider these best practices:

* **Use** `count` for Identical Resources:  
    When creating multiple instances of the same resource, use `count` to keep your code concise.
    
* **Prefer** `for_each` for Unique Items:  
    Use `for_each` when each resource instance is unique or when iterating over a collection with distinct keys.
    
* **Simplify with Conditionals:**  
    Leverage conditional expressions (`? :`) to make environment-based decisions clear and concise.
    
* **Utilize** `lookup()` to Avoid Hardcoding:  
    Dynamic map lookups help maintain flexibility and reduce hardcoded values in your configurations.
    
* **Employ Dynamic Blocks:**  
    Use dynamic blocks for nested configurations that need to adjust based on input variables or other dynamic data.
    

## Conclusion

Dynamic expressions in Terraform enable you to build adaptable, reusable, and efficient infrastructure configurations. By integrating variables, conditionals, loops, and lookups into your code, you can cater to varying deployment scenarios without rewriting or duplicating configurations. Embracing these techniques not only simplifies your code but also ensures that your infrastructure scales gracefully as requirements change.

Happy coding and automating with Terraform!

## Reference

1. **Terraform Expressions Documentation**  
    [https://www.terraform.io/language/expressions](https://www.terraform.io/language/expressions)  
    Detailed guidance on writing dynamic expressions in Terraform to generate flexible configurations.
    
2. **Terraform Conditional Expressions**  
    [https://www.terraform.io/language/expressions/conditionals](https://www.terraform.io/language/expressions/conditionals)  
    Learn how to implement if-else logic within your Terraform configurations to adapt resource definitions dynamically.
    
3. **Terraform Meta-Arguments: for\_each and count**  
    [https://www.terraform.io/language/meta-arguments/for\_each](https://www.terraform.io/language/meta-arguments/for_each)  
    Explains how to dynamically create multiple resources using the for\_each and count meta-arguments.
    
4. **Dynamic Blocks in Terraform**  
    [https://www.terraform.io/language/expressions/dynamic-blocks](https://www.terraform.io/language/expressions/dynamic-blocks)  
    Explore how to generate nested blocks dynamically to manage complex resource configurations.
    
5. **Terraform Best Practices**  
    [https://learn.hashicorp.com/tutorials/terraform/best-practices](https://learn.hashicorp.com/tutorials/terraform/best-practices)  
    A comprehensive tutorial on writing maintainable and efficient Terraform code, including strategies for dynamic expressions.