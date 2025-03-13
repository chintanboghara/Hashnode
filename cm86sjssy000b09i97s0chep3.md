---
title: "Terraform Associate: Output Data from Terraform"
seoTitle: "Outputting Data in Terraform Guide"
seoDescription: "Learn how to define, display, and secure Terraform outputs for dynamic infrastructure management and integration with external tools"
datePublished: Thu Mar 13 2025 03:30:18 GMT+0000 (Coordinated Universal Time)
cuid: cm86sjssy000b09i97s0chep3
slug: terraform-associate-output-data-from-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1740475221699/e9505b4b-c0d3-425f-89a4-3d649e260080.png
tags: cloud, devops, sre, terraform, devsecops, platform-engineering, iac-infrastructure-as-code, terraform-associate

---

Terraform outputs are a powerful feature that allows you to extract, display, and use information about your deployed infrastructure. Whether you need to retrieve an EC2 instance’s public IP, a database connection string, or a VPC ID to pass between modules, outputs make your infrastructure more transparent and dynamic.

In this guide, we’ll explore:

* How to define output variables.
    
* Displaying and retrieving outputs.
    
* Handling multiple values and sensitive outputs.
    
* Passing outputs between modules.
    
* Saving outputs for external use.
    
* Best practices for using outputs.
    

## 1\. Defining Output Variables

Output variables are defined using the `output` block in your Terraform configuration. They are useful for capturing and displaying important attributes from your resources.

### Example: Output an EC2 Instance’s Public IP

In your Terraform configuration (e.g., `outputs.tf`), you might define an output variable like this:

```plaintext
output "instance_public_ip" {
  description = "The public IP of the EC2 instance"
  value       = aws_instance.example.public_ip
}
```

After running your Terraform commands, this output will provide the public IP address of the EC2 instance that was created.

## 2\. Applying Terraform and Viewing Outputs

After applying your Terraform configuration, you can easily view the outputs.

### Steps:

1. **Apply the Configuration:**
    
    ```bash
    terraform apply
    ```
    
2. **View All Outputs:**
    
    ```bash
    terraform output
    ```
    
    **Example output:**
    
    ```plaintext
    instance_public_ip = "34.216.123.45"
    ```
    
3. **Retrieve a Specific Output:**
    
    ```bash
    terraform output instance_public_ip
    ```
    
    **Result:**
    
    ```plaintext
    34.216.123.45
    ```
    

This process allows you to quickly verify key infrastructure details directly from the CLI.

## 3\. Outputting Multiple Values

Terraform makes it easy to output multiple values, whether you’re dealing with a list of items or a map of values.

### Example: Output Multiple EC2 Instance IPs

If you have multiple instances, you can output all their public IPs as a list:

```plaintext
output "instance_ips" {
  description = "List of instance public IPs"
  value       = aws_instance.example[*].public_ip
}
```

**Example output:**

```plaintext
instance_ips = [
  "34.216.123.45",
  "35.172.85.10"
]
```

This approach is particularly useful for scaling or when you need to reference multiple resources simultaneously.

## 4\. Marking Outputs as Sensitive

Outputs that contain sensitive information, such as passwords or private keys, should be protected to prevent exposure.

### Example: Masking a Sensitive Output

```plaintext
output "db_password" {
  description = "Database password"
  value       = aws_db_instance.example.password
  sensitive   = true
}
```

When you run:

```bash
terraform output
```

The sensitive value will be masked:

```plaintext
db_password = <sensitive>
```

**Important:** Marking an output as sensitive prevents it from being displayed in plain text but does not remove it from the Terraform state file.

## 5\. Using Outputs in Other Terraform Modules

Outputs can be used as inputs for other modules, allowing you to pass values dynamically between different parts of your configuration.

### Example: Passing Outputs Between Modules

#### Module 1 (`vpc/main.tf`)

```plaintext
output "vpc_id" {
  description = "VPC ID"
  value       = aws_vpc.main.id
}
```

#### Module 2 (`ec2/main.tf`)

```plaintext
module "vpc" {
  source = "../vpc"
}

resource "aws_instance" "example" {
  # Use the VPC ID output from the VPC module
  vpc_security_group_ids = [module.vpc.vpc_id]
}
```

This modular approach keeps your configurations clean and promotes reuse across environments.

## 6\. Saving Terraform Outputs for External Use

Outputs can be saved and utilized outside of Terraform, which is useful for automation, integration with other tools, or simple record-keeping.

### a) Save Outputs to a JSON File

Use the `terraform output -json` command to export outputs in JSON format:

```bash
terraform output -json > terraform_outputs.json
```

**Example JSON output:**

```json
{
  "instance_public_ip": {
    "value": "34.216.123.45",
    "type": "string"
  }
}
```

### b) Use Outputs in a Shell Script

Retrieve an output value directly in a shell script for automation:

```bash
INSTANCE_IP=$(terraform output -raw instance_public_ip)
echo "Instance IP: $INSTANCE_IP"
```

This makes it easy to integrate Terraform outputs into your CI/CD pipelines or other automation workflows.

## 7\. Best Practices for Terraform Outputs

* **Retrieve Essential Details:** Use outputs to capture crucial information like IP addresses, resource IDs, and endpoints.
    
* **Protect Sensitive Data:** Mark outputs as `sensitive` to prevent exposure of sensitive information.
    
* **Promote Reusability:** Pass outputs between modules to maintain modular and reusable configurations.
    
* **Automate with JSON:** Save outputs in JSON format when integrating with external tools or scripts.
    
* **Keep It Clean:** Only output the information that is necessary for downstream processes or user visibility.
    

## Conclusion

Terraform outputs are a versatile tool for extracting and using information about your deployed infrastructure. By defining and managing outputs properly, you can:

* Easily verify resource attributes.
    
* Pass critical data between modules.
    
* Secure sensitive information.
    
* Integrate Terraform with other tools and workflows.
    

Implementing these practices helps ensure that your infrastructure is not only robust but also transparent and adaptable. Happy Terraforming!

## Reference

1. [Terraform Outputs Documentation](https://www.terraform.io/language/values/outputs)  
    *Dive into the official Terraform documentation to understand how to define and manage output variables in your configurations.*
    
2. [Terraform CLI Output Command](https://developer.hashicorp.com/terraform/cli/commands/output)  
    *Explore the usage and options of the* `terraform output` command for retrieving and formatting your infrastructure data.
    
3. [Terraform Modules: Using Outputs](https://www.terraform.io/language/modules/outputs)  
    *Learn how to pass outputs between modules to create modular, reusable, and maintainable Terraform configurations.*
    
4. [Securing Sensitive Data in Terraform](https://www.terraform.io/language/values/variables#sensitive-variables)  
    *Understand best practices for marking outputs as sensitive to protect critical information from exposure.*
    
5. [Automating Workflows with Terraform JSON Outputs](https://developer.hashicorp.com/terraform/cli/commands/output#json-format)  
    *Discover how to export Terraform outputs in JSON format for seamless integration with external tools and CI/CD pipelines.*