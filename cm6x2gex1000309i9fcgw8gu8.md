---
title: "Terraform Associate: Lock and upgrade provider versions"
seoTitle: "Locking and Upgrading Terraform Provider Versions"
seoDescription: "Learn how to lock and upgrade provider versions in Terraform to ensure consistency, prevent breaking changes, and maintain secure infrastructure"
datePublished: Sun Feb 09 2025 03:30:12 GMT+0000 (Coordinated Universal Time)
cuid: cm6x2gex1000309i9fcgw8gu8
slug: terraform-associate-lock-and-upgrade-provider-versions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1738211421287/1a4abb34-4e85-426c-be99-b8bad17667b5.png
tags: cloud, devops, sre, terraform, devsecops, platform-engineering, terraform-associate

---

In Terraform, it's important to use the right version of a provider to prevent breaking changes or inconsistencies across environments. You can do this by **locking the provider version** in your configuration and making sure it can be upgraded or updated when needed.

## Locking Provider Versions

Terraform lets you set a version constraint for the providers in your configuration files. This ensures that Terraform will only use a specific version or range of versions of the provider, preventing unexpected behavior from updates or changes in the provider.

Here’s how you can lock the provider version in Terraform:

### 1\. **Provider Block Version Constraints**

The version of a provider can be specified using version constraints in the `provider` block, typically within your `main.tf` or a separate `providers.tf` file.

Example of how to lock a specific version of a provider:

```plaintext
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "4.10.0"
    }
  }
}

provider "aws" {
  region = "us-west-2"
}
```

In this example:

* `source` specifies the provider's registry (the source of the provider).
    
* `version` specifies the exact version of the AWS provider to use.
    

#### **Version Constraints Format**

You can use different types of version constraints depending on your need:

* **Exact Version**:  
    If you want to lock to a specific version, such as `4.10.0`, you can use:
    
    ```plaintext
    version = "4.10.0"
    ```
    
* **Version Range**:  
    To specify a version range, you can use operators like `>=`, `<=`, `~>` (which allows upgrading within minor versions), etc.
    
    * Allow any version greater than or equal to 4.0.0 but less than 5.0.0:
        
        ```plaintext
        version = ">= 4.0.0, < 5.0.0"
        ```
        
    * Allow versions that are compatible with `4.10.x` (for example, any 4.10.x version):
        
        ```plaintext
        version = "~> 4.10.0"
        ```
        
    * Allow versions starting from `4.0.0` or higher:
        
        ```plaintext
        version = ">= 4.0.0"
        ```
        

### 2\. **Provider Lock File (**`.terraform.lock.hcl`)

Terraform uses a lock file (`.terraform.lock.hcl`) to track the exact versions of providers that were installed and used during the last run. This ensures that the same version is used across different environments and machines, providing consistency.

To initialize or update the provider and create the lock file, you can use:

```bash
terraform init
```

If you want to upgrade the provider to a newer version within the specified constraints, run:

```bash
terraform providers lock
```

Terraform will update the `.terraform.lock.hcl` file to reflect the versions that are being used.

### 3\. **Upgrading Providers**

To upgrade the provider version while keeping the version constraint, you can run the following command:

```bash
terraform init -upgrade
```

This command tells Terraform to upgrade the providers to the latest acceptable versions according to the version constraints defined in your configuration.

## Example of Locking and Upgrading Providers

Let’s say you want to lock the `aws` provider to versions between `3.0.0` and `4.0.0`, but later decide you need to upgrade it to a newer version. Here’s how the configuration might look:

1. **Locking the Provider Version:**
    

```plaintext
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = ">= 3.0.0, < 4.0.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}
```

2. **Upgrading the Provider:** After realizing you need a new feature available only in version `4.0.0` and later, modify the version constraint to:
    

```plaintext
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = ">= 4.0.0"
    }
  }
}
```

Then run:

```bash
terraform init -upgrade
```

This will upgrade the `aws` provider to a version that satisfies the new constraint.

## Why Locking and Upgrading Provider Versions Matters

1. **Consistency Across Environments**: Locking provider versions ensures your infrastructure works the same on different machines, teams, and environments. Without version locking, each Terraform run might use a different provider version, causing unexpected changes or behavior.
    
2. **Prevent Breaking Changes**: Providers can introduce breaking changes or new features in major or minor versions. By locking the version, you avoid unexpected disruptions in your infrastructure when the provider is updated.
    
3. **Security and Bug Fixes**: While locking the version is important, it's also necessary to upgrade providers regularly to get security patches, bug fixes, and new features that improve functionality and stability.
    

## Conclusion

Locking and upgrading provider versions in Terraform is essential to ensure consistent, predictable, and secure infrastructure management. Using version constraints allows you to have control over which provider versions are used, while the `.terraform.lock.hcl` file provides the practical mechanism to enforce that version in all environments. Periodically upgrading providers ensures your infrastructure is up-to-date and secure.

## Reference

1. [https://www.terraform.io/docs/language/providers/requirements.html](https://www.terraform.io/docs/language/providers/requirements.html)  
    Terraform's official documentation on provider versioning and constraints, explaining how to lock and upgrade provider versions.
    
2. [https://registry.terraform.io/](https://registry.terraform.io/)  
    The official Terraform provider registry where you can explore various providers and their versions to include in your configurations.
    
3. [https://www.hashicorp.com/blog/lock-terraform-provider-versions](https://www.hashicorp.com/blog/lock-terraform-provider-versions)  
    A blog post by HashiCorp that explains how to lock provider versions and why it is important for Terraform users.
    
4. [https://learn.hashicorp.com/tutorials/terraform/provider-upgrade?in=terraform/providers](https://learn.hashicorp.com/tutorials/terraform/provider-upgrade?in=terraform/providers)  
    A tutorial on how to upgrade Terraform providers while maintaining your version constraints, ensuring you’re using the latest compatible versions.
    
5. [https://www.terraform.io/docs/state/](https://www.terraform.io/docs/state/)  
    A guide on how Terraform state interacts with provider versions, and why managing versions and lock files is crucial for stability.