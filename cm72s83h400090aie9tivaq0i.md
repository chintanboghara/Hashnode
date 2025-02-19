---
title: "Terraform Associate: Build Infrastructure"
seoTitle: "Terraform Basics: Build Infrastructure"
seoDescription: "Build and manage cloud infrastructure with Terraform using declarative configuration files and provider APIs in this step-by-step guide"
datePublished: Thu Feb 13 2025 03:30:25 GMT+0000 (Coordinated Universal Time)
cuid: cm72s83h400090aie9tivaq0i
slug: terraform-associate-build-infrastructure
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1738211510845/f7a6f745-4294-43d6-8055-5803cdba0eb6.png
tags: cloud, devops, sre, terraform, devsecops, platform-engineering, iac-infrastructure-as-code, terraform-associate

---

Building infrastructure with Terraform means creating resources like virtual machines, networks, databases, and other services in cloud environments (such as AWS, Azure, GCP, etc.) using declarative configuration files. After defining the infrastructure, Terraform sets it up and manages it by interacting with the cloud provider APIs.

Here’s a step-by-step guide to building infrastructure with Terraform:

## 1\. **Install Terraform**

First, you need to install Terraform on your system. You can download it from the official website: [Terraform Downloads](https://www.terraform.io/downloads).

To check if Terraform is installed correctly, run:

```bash
terraform --version
```

## 2\. **Set Up Your Project Directory**

Create a new directory for your Terraform project and navigate to it:

```bash
mkdir my-terraform-infrastructure
cd my-terraform-infrastructure
```

## 3\. **Create Terraform Configuration Files**

Terraform configuration files are written in **HCL (HashiCorp Configuration Language)** and typically have an `.tf` extension.

Let’s say you want to build infrastructure in AWS (Amazon Web Services). The first step is to configure the AWS provider and define the resources you want to create, such as an EC2 instance and a security group.

### Example of Terraform Configuration

Here’s a simple Terraform configuration to create an AWS EC2 instance with a security group.

1. **Define the AWS Provider (**[**providers.tf**](http://providers.tf)**)**: This file specifies the cloud provider (AWS in this case) and the region.
    
    ```plaintext
    provider "aws" {
      region = "us-west-2"  # Specify your desired region
    }
    ```
    
2. **Define Resources (**[**main.tf**](http://main.tf)**)**: In this file, you define the actual resources you want to create. For example, an EC2 instance and a security group.
    
    ```plaintext
    resource "aws_security_group" "allow_ssh" {
      name        = "allow_ssh"
      description = "Allow SSH inbound traffic"
      
      ingress {
        from_port   = 22
        to_port     = 22
        protocol    = "tcp"
        cidr_blocks = ["0.0.0.0/0"]
      }
    
      egress {
        from_port   = 0
        to_port     = 0
        protocol    = "-1"
        cidr_blocks = ["0.0.0.0/0"]
      }
    }
    
    resource "aws_instance" "example" {
      ami           = "ami-0c55b159cbfafe1f0"  # Replace with a valid AMI ID
      instance_type = "t2.micro"
      key_name      = "my-key-pair"  # Replace with your SSH key name
      
      security_groups = [aws_security_group.allow_ssh.name]
    }
    ```
    

In this configuration:

* We define an **AWS provider** that specifies which region to use.
    
* We define a **security group** (`aws_security_group.allow_ssh`) that allows SSH traffic on port 22.
    
* We create an **EC2 instance** (`aws_instance.example`) with a specified AMI and instance type (`t2.micro`). The instance is also associated with the security group we created.
    

3. **Create a** `terraform.tfvars` file (optional): If you want to pass variables like AWS credentials, region, or instance type, you can define a `terraform.tfvars` file.
    
    ```plaintext
    region = "us-west-2"
    ami_id = "ami-0c55b159cbfafe1f0"
    instance_type = "t2.micro"
    ```
    

## 4\. **Initialize the Terraform Project**

Before you can use Terraform to manage your infrastructure, you need to initialize your project. Run the following command to initialize the working directory and download the necessary provider plugins:

```bash
terraform init
```

This command sets up the environment and prepares Terraform to interact with your cloud provider.

## 5\. **Preview the Infrastructure Changes**

Use the `terraform plan` command to preview the changes Terraform will make. It will show you which resources will be created, updated, or deleted based on your configuration.

```bash
terraform plan
```

This will display a detailed output, like:

```plaintext
+ aws_security_group.allow_ssh
+ aws_instance.example
```

## 6\. **Apply the Changes (Build Infrastructure)**

After reviewing the plan, you can apply the configuration to create the infrastructure:

```bash
terraform apply
```

Terraform will ask for confirmation before proceeding with the infrastructure creation. Type `yes` to proceed.

Terraform will then proceed to create the resources specified in your configuration file. It will interact with the AWS API (or your chosen provider) to create the infrastructure.

## 7\. **Verify the Infrastructure**

Once the `terraform apply` command finishes, Terraform will output information about the created resources. You can verify your infrastructure by logging into your AWS Console (or your respective cloud provider console) and confirming that the resources (like EC2 instances, security groups, etc.) are created.

For instance, you should be able to see the EC2 instance under the "Instances" section and the security group under "Security Groups" in AWS.

## 8\. **Managing Infrastructure State**

Terraform manages the current state of your infrastructure in a file called `terraform.tfstate`. This file keeps track of the resources you have created and their state in the cloud. It is crucial to manage this state file properly. Terraform uses this state to compare your current infrastructure with your desired state when you run commands like `terraform plan` and `terraform apply`.

## 9\. **Updating Infrastructure**

If you want to modify your infrastructure, simply update the configuration files. For example, if you want to change the instance type, modify the `instance_type` in the `aws_instance` block and then run:

```bash
terraform plan
terraform apply
```

Terraform will calculate the changes and apply the necessary updates to your infrastructure.

## 10\. **Destroying Infrastructure**

If you want to tear down the infrastructure you’ve built, you can use the `terraform destroy` command. This will remove all resources defined in the configuration files.

```bash
terraform destroy
```

Again, Terraform will prompt for confirmation before it deletes the resources. Type `yes` to destroy them.

## Conclusion

Building infrastructure with Terraform involves defining your resources in configuration files, initializing the Terraform project, running `terraform plan` to preview changes, and applying those changes with `terraform apply`. Terraform automates the process of provisioning infrastructure, ensuring consistency, repeatability, and version control.

By following these steps, you can easily build, manage, and scale infrastructure on any cloud platform supported by Terraform, all while keeping infrastructure management as code.

## Reference

1. [https://learn.hashicorp.com/tutorials/terraform/install-cli](https://learn.hashicorp.com/tutorials/terraform/install-cli)  
    Official guide for installing Terraform on different operating systems and checking if the installation is successful.
    
2. [https://www.terraform.io/docs/language/index.html](https://www.terraform.io/docs/language/index.html)  
    Complete documentation on Terraform's HashiCorp Configuration Language (HCL) for writing infrastructure as code.
    
3. [https://aws.amazon.com/blogs/infrastructure-and-automation/introducing-terraform-quick-starts-for-aws/](https://aws.amazon.com/blogs/infrastructure-and-automation/introducing-terraform-quick-starts-for-aws/)  
    A useful introduction to using Terraform on AWS, including key concepts and examples for creating cloud resources.
    
4. [https://www.terraform.io/docs/cli/index.html](https://www.terraform.io/docs/cli/index.html)  
    A detailed reference for all Terraform commands like `terraform init`, `terraform plan`, and `terraform apply`, which are essential for managing your infrastructure.
    
5. [https://www.terraform.io/docs/language/state/index.html](https://www.terraform.io/docs/language/state/index.html)  
    A guide on understanding and managing Terraform state files, ensuring consistent and reliable infrastructure management across different environments.