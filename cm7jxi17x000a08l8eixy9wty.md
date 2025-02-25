---
title: "Terraform Associate: Apply Terraform Configuration"
seoTitle: "Mastering Terraform: Apply Configuration Basics"
seoDescription: "Learn how to apply Terraform configurations, ensuring your infrastructure aligns with your plans through a detailed workflow and best practices"
datePublished: Tue Feb 25 2025 03:30:12 GMT+0000 (Coordinated Universal Time)
cuid: cm7jxi17x000a08l8eixy9wty
slug: terraform-associate-apply-terraform-configuration
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1739926160905/779a3792-7594-4230-a71a-20e89f6ec579.png
tags: cloud, devops, sre, terraform, devsecops, platform-engineering, iac-infrastructure-as-code, terraform-associate

---

After crafting and reviewing your Terraform plan, the final step in provisioning your infrastructure is to apply the configuration using the `terraform apply` command. This command takes your configuration files and the planned changes, then executes the necessary actions to create, modify, or delete resources. Let’s dive into what happens during this process and explore a detailed workflow for applying your Terraform configuration.

## What Does `terraform apply` Do?

When you run `terraform apply`, Terraform performs the following actions:

1. **Recalculates the Desired State:**  
    Terraform reads your configuration files and compares the desired state with the current state stored in your state file (`terraform.tfstate`).
    
2. **Executes Necessary Actions:**  
    Based on the differences between the current and desired states, Terraform creates, modifies, or destroys resources to match your configuration.
    
3. **Updates the State File:**  
    Once the changes are made, Terraform updates the state file to reflect the new status of your infrastructure.
    

This process ensures that your live infrastructure aligns with your configuration, making your deployments predictable and consistent.

## Steps to Apply a Terraform Configuration

### 1\. Ensure Terraform Is Initialized

Before applying any changes, make sure your Terraform environment is properly initialized. This ensures that all required provider plugins are installed and the backend is configured.

```bash
terraform init
```

### 2\. Create or Review the Terraform Plan

It’s best practice to run `terraform plan` before applying changes. This step previews what Terraform will do and helps you catch any unexpected modifications.

```bash
terraform plan
```

Review the output carefully to understand which resources will be created, modified, or destroyed.

### 3\. Run `terraform apply`

Once you’re satisfied with the plan, run the following command to apply the configuration:

```bash
terraform apply
```

Terraform will display the execution plan again and prompt for confirmation. You’ll see output similar to:

```plaintext
Terraform will perform the following actions:

  # aws_instance.example will be created
  + resource "aws_instance" "example" {
      + ami           = "ami-0c55b159cbfafe1f0"
      + id            = (known after apply)
      + instance_type = "t2.micro"
      + ...
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
Only 'yes' will be accepted to approve.
  Enter a value: 
```

### 4\. Confirm the Apply Action

Type `yes` to confirm and proceed with applying the changes:

```plaintext
Enter a value: yes
```

If you type anything else, Terraform will cancel the apply operation as a safeguard against accidental modifications.

### 5\. Terraform Applies the Changes

Once confirmed, Terraform executes the necessary actions. You will see progress output indicating the status of each resource, for example:

```plaintext
aws_instance.example: Creating...
aws_instance.example: Still creating... [10s elapsed]
aws_instance.example: Creation complete after 15s [id=i-0a123b4567c89d012]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

### 6\. Verify the Infrastructure

After the apply operation completes, verify that the changes have been successfully implemented:

* **Cloud Provider Dashboard:**  
    Log into the AWS Management Console (or your respective provider’s dashboard) to confirm that the EC2 instance or other resources have been created or updated as expected.
    
* **State Verification:**  
    Use the `terraform show` command to inspect the current state in a human-readable format:
    
    ```bash
    terraform show
    ```
    

### 7\. Optional: Apply a Saved Plan

If you previously saved a plan using:

```bash
terraform plan -out=tfplan
```

You can apply the saved plan directly:

```bash
terraform apply tfplan
```

This ensures that the exact set of changes you reviewed is applied to your infrastructure.

## Example Workflow: Applying a Terraform Configuration

Let’s review a typical workflow from configuration to deployment:

1. **Write Your Configuration (**[`main.tf`](http://main.tf)):
    
    ```plaintext
    provider "aws" {
      region = "us-west-2"
    }
    
    resource "aws_instance" "example" {
      ami           = "ami-0c55b159cbfafe1f0"
      instance_type = "t2.micro"
    }
    ```
    
2. **Initialize the Environment:**
    
    ```bash
    terraform init
    ```
    
3. **Generate and Review the Plan:**
    
    ```bash
    terraform plan
    ```
    
4. **Apply the Configuration:**
    
    ```bash
    terraform apply
    ```
    
5. **Confirm the Changes:**  
    Type `yes` when prompted.
    
6. **Verify the Infrastructure:**  
    Check your AWS console or run `terraform show` to review the updated state.
    

## Conclusion

Applying a Terraform configuration using `terraform apply` is the final and critical step in the Terraform workflow. It transforms your written configuration into actual infrastructure changes by creating, modifying, or destroying resources, and then updates the state file to reflect these changes. By following the outlined steps—initializing your environment, reviewing the plan, confirming the execution, and verifying the results—you can confidently manage your infrastructure with Terraform.

Happy Terraforming!

## Reference

1. [Terraform Apply Command Documentation](https://developer.hashicorp.com/terraform/cli/commands/apply)  
    *Dive into the detailed options and behavior of the* `terraform apply` command to understand how Terraform implements your configuration changes.
    
2. [Terraform Getting Started Guide](https://learn.hashicorp.com/collections/terraform/aws-get-started)  
    *A beginner-friendly guide that walks you through initializing, planning, and applying Terraform configurations in real-world cloud environments.*
    
3. [Terraform State Management](https://www.terraform.io/language/state)  
    *Learn how Terraform manages and updates its state file during the apply process, ensuring your infrastructure reflects your configuration accurately.*
    
4. [Understanding Terraform Workflow](https://developer.hashicorp.com/terraform/tutorials/automating-aws)  
    *Explore a complete workflow from configuration to deployment, including the steps to initialize, plan, and apply your Terraform changes.*
    
5. [Terraform CLI Commands Overview](https://developer.hashicorp.com/terraform/cli)  
    *Get an overview of all Terraform CLI commands to better understand how each fits into your infrastructure provisioning workflow.*