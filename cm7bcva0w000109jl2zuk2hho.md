---
title: "Terraform Associate: Store Remote State"
seoTitle: "Remote State Storage with Terraform"
seoDescription: "Learn how to set up remote state storage in Terraform with AWS S3 and DynamoDB for improved collaboration, security, and infrastructure management"
datePublished: Wed Feb 19 2025 03:30:29 GMT+0000 (Coordinated Universal Time)
cuid: cm7bcva0w000109jl2zuk2hho
slug: terraform-associate-store-remote-state
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1739079040280/80a058d9-06ac-47a6-9fa3-806633d4c13c.png
tags: cloud, devops, sre, terraform, devsecops, platform-engineering, iac-infrastructure-as-code, terraform-associate

---

In today’s dynamic cloud environments, managing infrastructure efficiently is key to success. Terraform, a powerful Infrastructure as Code (IaC) tool, manages your infrastructure state using a state file (`terraform.tfstate`). By default, this state file is stored locally. However, for teams and production environments, storing state remotely is crucial for collaboration, consistency, and security.

In this blog post, we’ll explore the benefits of remote state storage, walk through the steps to set it up using AWS S3 and DynamoDB, and discuss best practices to ensure your state remains secure and reliable.

## Why Store Remote State?

Before diving into the setup process, let’s review some of the primary benefits of storing Terraform state remotely:

* **Collaboration:**  
    When your state file is stored in a centralized location, multiple team members can work on the same infrastructure concurrently. Everyone accesses the same state, reducing the risk of conflicts and configuration drift.
    
* **State Locking:**  
    Many remote backends (such as AWS S3 with DynamoDB) support state locking. This feature prevents concurrent modifications, ensuring that only one person or process can change the state at any given time.
    
* **Consistency:**  
    A centralized state file is accessible from various environments or machines, ensuring that your infrastructure’s state remains consistent across the board.
    
* **Security:**  
    Sensitive data—such as passwords or API keys—can be better protected when stored in a secure remote backend with encryption and strict access controls.
    

## Step-by-Step Guide to Storing Remote State in Terraform

### 1\. Choose a Backend

Terraform supports multiple backend options for remote state storage. Some popular choices include:

* **Amazon S3** (AWS)
    
* **Azure Blob Storage** (Azure)
    
* **Google Cloud Storage (GCS)** (Google Cloud)
    
* **Terraform Cloud** (HashiCorp’s managed service)
    
* **Consul** (for advanced use cases)
    

For this guide, we’ll use **AWS S3** with **DynamoDB** for state locking.

### 2\. Set Up the Remote Backend (AWS S3 with DynamoDB)

#### a) Create an S3 Bucket for Terraform State

Your first step is to create an S3 bucket where Terraform will store its state file. You can use the AWS Console or AWS CLI. For example, to create a bucket using the CLI:

```bash
aws s3 mb s3://my-terraform-state-bucket
```

*Note:* Ensure the bucket name is globally unique.

#### b) Create a DynamoDB Table for State Locking

State locking is vital to prevent multiple users from updating the state file simultaneously. Create a DynamoDB table with a primary key to uniquely identify locks.

Using the AWS Console is straightforward, but here’s how you can do it with the AWS CLI:

```bash
aws dynamodb create-table \
  --table-name terraform-locks \
  --attribute-definitions AttributeName=LockID,AttributeType=S \
  --key-schema AttributeName=LockID,KeyType=HASH \
  --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5
```

#### c) Configure the Remote Backend in Terraform

Within your Terraform project, create or update a file (e.g., [`backend.tf`](http://backend.tf)) to configure the S3 backend. Include the bucket name, path to the state file, AWS region, DynamoDB table for locking, and encryption settings.

```plaintext
terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"   # S3 bucket name
    key            = "path/to/my/terraform.tfstate"  # Path within the bucket
    region         = "us-west-2"                     # AWS region
    dynamodb_table = "terraform-locks"               # DynamoDB table for state locking
    encrypt        = true                            # Enable encryption for security
  }
}
```

#### d) Initialize Terraform with the Remote Backend

After configuring your backend, initialize Terraform to set up and, if necessary, migrate your local state to the remote backend.

```bash
terraform init
```

Terraform will detect the backend configuration, initialize it, and prompt you to migrate your local state if needed. Simply type `yes` when prompted.

### 3\. Verify Remote State Storage

After initialization, Terraform will use your remote backend for storing and locking state. To verify that everything is set up correctly, run:

```bash
terraform state list
```

This command should list all resources managed by Terraform, confirming that the remote state is active.

### 4\. Working with Remote State

Once remote state is configured, your typical Terraform commands interact with the remote backend seamlessly:

* **terraform apply:**  
    Applies changes to your infrastructure while updating the remote state.
    
* **terraform plan:**  
    Compares your local configuration with the remote state to compute necessary changes.
    
* **State Locking:**  
    During operations like `terraform apply`, the state file is locked in DynamoDB to prevent simultaneous modifications. If another process attempts to run an operation concurrently, it will receive a message indicating that the state is locked.
    

### 5\. Handling Remote State in a Team Environment

For teams, consistency and coordination are paramount:

* **Unified Backend Configuration:**  
    Ensure all team members use the same [`backend.tf`](http://backend.tf) configuration to point to the remote state.
    
* **Workspaces:**  
    Use Terraform workspaces to manage different environments (e.g., development, staging, production) with separate state files. This allows you to segregate environments while using the same configuration.
    
* **Access Controls:**  
    Leverage IAM roles and policies to restrict who can read or modify the state file. Enabling server-side encryption (like S3 encryption) further secures sensitive data within the state.
    

## Security Considerations

When storing remote state, keep the following security practices in mind:

* **State File Encryption:**  
    Enable encryption for your state file. For AWS, the `encrypt = true` setting ensures that data is encrypted using S3’s server-side encryption.
    
* **Access Management:**  
    Control access to both the S3 bucket and the DynamoDB table using fine-grained IAM policies. This minimizes the risk of unauthorized modifications.
    
* **Sensitive Data Handling:**  
    Be cautious about the sensitive information contained in your state file. If possible, avoid storing secrets or passwords directly in your Terraform configurations.
    

## Conclusion

Storing remote state in Terraform is essential for teams and production environments. It ensures collaboration, prevents conflicting changes through state locking, and secures your infrastructure’s state data. By following this guide—choosing an appropriate backend, setting up S3 and DynamoDB for state and locking, configuring your Terraform project, and applying best security practices—you can manage your infrastructure state confidently and securely.

Embrace remote state to elevate your Terraform workflow, enhance team collaboration, and maintain a robust, secure infrastructure environment.

Happy Terraforming!

## Reference

1. [Terraform Backends Configuration](https://www.terraform.io/language/settings/backends/configuration)  
    *Learn how to configure remote backends in Terraform, including setting up S3 and DynamoDB for state storage and locking.*
    
2. [Creating an S3 Bucket](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html)  
    *A comprehensive guide by AWS on how to create an S3 bucket, an essential step for storing your Terraform state remotely.*
    
3. [Getting Started with DynamoDB Tables](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GettingStarted.CreateTable.html)  
    *Step-by-step instructions on creating a DynamoDB table, which is used for state locking in Terraform to prevent concurrent modifications.*
    
4. [Terraform State Management](https://www.terraform.io/language/state)  
    *Detailed information on how Terraform manages state, including best practices for security, encryption, and consistency.*
    
5. [Terraform Workspaces](https://www.terraform.io/language/state/workspaces)  
    *Discover how Terraform workspaces can be used to manage multiple environments and separate state files, enhancing collaboration and organization.*