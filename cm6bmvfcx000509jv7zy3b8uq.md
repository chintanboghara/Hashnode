---
title: "Mastering Terraform: Essential Commands and State Management Guide"
seoTitle: "Terraform: Commands & State Management"
seoDescription: "Learn essential Terraform commands, state management, workspaces, and best practices for confident infrastructure management"
datePublished: Sat Jan 25 2025 03:30:49 GMT+0000 (Coordinated Universal Time)
cuid: cm6bmvfcx000509jv7zy3b8uq
slug: mastering-terraform-essential-commands-and-state-management-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1737543112821/47900802-3908-46f7-8c8c-9efc9a873f82.png
tags: cloud, devops, sre, terraform, devsecops, platform-engineering

---

## Core Commands

* `terraform init`: Initializes a working directory containing Terraform configuration files. Downloads required providers and configures the backend.
    
    ```bash
    terraform init
    ```
    
* `terraform plan`: Generates an execution plan showing proposed infrastructure changes.
    
    ```bash
    terraform plan
    ```
    
* `terraform apply`: Applies changes to reach the desired infrastructure state. Use `-auto-approve` to skip confirmation.
    
    ```bash
    terraform apply  # Interactive mode
    terraform apply -auto-approve  # Skip prompt
    ```
    
* `terraform destroy`: Destroys all managed infrastructure. Use with caution!
    
    ```bash
    terraform destroy  # Interactive mode
    terraform destroy -auto-approve  # Skip prompt
    ```
    
* `terraform validate`: Checks configuration files for syntax and consistency.
    
    ```bash
    terraform validate
    ```
    
* `terraform fmt`: Rewrites configuration files to a standardized format.
    
    ```bash
    terraform fmt
    ```
    
* `terraform show`: Displays the current state or a saved plan in readable format.
    
    ```bash
    terraform show
    ```
    
* `terraform output`: Prints output values from the state file.
    
    ```bash
    terraform output
    ```
    
* `terraform refresh`: Syncs the state file with real-world infrastructure (rarely used directly).
    
    ```bash
    terraform refresh
    ```
    

## State Management Commands

* `terraform state list`: Lists resources tracked in the state.
    
    ```bash
    terraform state list
    ```
    
* `terraform state show <resource>`: Displays details of a specific resource. Replace `<resource>` with the resource address.
    
    ```bash
    terraform state show aws_instance.web
    ```
    
* `terraform state pull`: Outputs the raw state data.
    
    ```bash
    terraform state pull > state.json
    ```
    
* `terraform state push`: Overwrites remote state with a local state file (**use with caution**).
    
    ```bash
    terraform state push terraform.tfstate
    ```
    
* `terraform state mv`: Moves a resource within the state (useful for refactoring).
    
    ```bash
    terraform state mv aws_instance.old aws_instance.new
    ```
    
* `terraform state rm`: Removes a resource from the state (does not destroy the resource).
    
    ```bash
    terraform state rm aws_instance.web
    ```
    
* `terraform import <resource> <id>`: Imports existing infrastructure into the state.
    
    ```bash
    terraform import aws_instance.web i-1234567890abcdef0
    ```
    

## Workspace Commands

* `terraform workspace new <name>`: Creates a new workspace.
    
    ```bash
    terraform workspace new dev
    ```
    
* `terraform workspace select <name>`: Switches to a workspace.
    
    ```bash
    terraform workspace select prod
    ```
    
* `terraform workspace list`: Lists all workspaces.
    
    ```bash
    terraform workspace list
    ```
    
* `terraform workspace delete <name>`: Deletes a workspace.
    
    ```bash
    terraform workspace delete staging
    ```
    

## Utility Commands

* `terraform version`: Shows Terraform and provider versions.
    
    ```bash
    terraform version
    ```
    
* `terraform get`: Downloads and updates modules.
    
    ```bash
    terraform get
    ```
    
* `terraform graph`: Generates a visual dependency graph.
    
    ```bash
    terraform graph | dot -Tsvg > graph.svg
    ```
    
* `terraform taint <resource>`: Forces recreation of a resource on the next apply.
    
    ```bash
    terraform taint aws_instance.web
    ```
    
* `terraform untaint <resource>`: Removes taint from a resource.
    
    ```bash
    terraform untaint aws_instance.web
    ```
    

## Advanced Commands

* `terraform force-unlock <lock-id>`: Manually releases a stuck state lock.
    
    ```bash
    terraform force-unlock 3a0d98d0-0d1a-2345-6789-abc123def456
    ```
    
* `terraform console`: Launches an interactive console for testing expressions.
    
    ```bash
    terraform console
    ```
    
* `terraform providers`: Displays provider configurations.
    
    ```bash
    terraform providers
    ```
    
* `terraform state replace-provider`: Updates the provider in the state file.
    
    ```bash
    terraform state replace-provider hashicorp/aws registry.acme.corp/acme/aws
    ```
    

## Environment Variables

* `TF_LOG`: Sets logging verbosity (e.g., `TRACE`, `DEBUG`, `INFO`).
    
    ```bash
    export TF_LOG=DEBUG
    ```
    
* `TF_VAR_<variable_name>`: Sets a Terraform variable via the environment.
    
    ```bash
    export TF_VAR_region="us-west-2"
    ```
    
* `TF_CLI_ARGS`: Passes global CLI arguments.
    
    ```bash
    export TF_CLI_ARGS="-input=false"
    ```
    
* `TF_IN_AUTOMATION`: Suppresses prompts in CI/CD environments.
    
    ```bash
    export TF_IN_AUTOMATION=true
    ```
    

> **Note**: Always review Terraform plans carefully before applying changes. Use destructive commands like `destroy` and `state push` with caution.

## Reference

1. **Terraform Official Documentation**  
    [https://developer.hashicorp.com/terraform/docs](https://developer.hashicorp.com/terraform/docs)  
    This is the official documentation for Terraform, covering how to install, configure, use commands, and follow best practices.
    
2. **Terraform CLI Commands Reference**  
    [https://developer.hashicorp.com/terraform/cli/commands](https://developer.hashicorp.com/terraform/cli/commands)  
    A detailed guide to all Terraform CLI commands, including descriptions, flags, and examples.
    
3. **Terraform State Management**  
    [https://developer.hashicorp.com/terraform/language/state](https://developer.hashicorp.com/terraform/language/state)  
    The official guide for managing state files in Terraform, with commands for listing, importing, and modifying state.
    
4. **Terraform Workspaces**  
    [https://developer.hashicorp.com/terraform/cloud-docs/workspaces](https://developer.hashicorp.com/terraform/cloud-docs/workspaces)  
    An in-depth guide on using Terraform workspaces to manage multiple environments.
    
5. **Terraform Environment Variables**  
    [https://developer.hashicorp.com/terraform/cli/config/environment-variables](https://developer.hashicorp.com/terraform/cli/config/environment-variables)  
    A comprehensive list of environment variables supported by Terraform, including usage examples.