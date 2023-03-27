Terragrunt is a thin wrapper for Terraform that provides extra tools for working with multiple Terraform modules, remote state, and locking. It also provides a powerful and flexible way to hierarchically provide configuration to Terraform, without duplicating code across environments, AWS regions, and AWS accounts – [keeping your Terraform config DRY](https://blog.gruntwork.io/terragrunt-how-to-keep-your-terraform-code-dry-and-maintainable-f61ae06959d8?gi=703957a5f669).

![Managing Terraform config across accounts, regions, and environments with Terragrunt](https://camillovisini.com/assets/xw2Bs7NbKJ-600.62a0182c.jpeg)

The following hierarchy is proposed (aligned with directory structure):

└── `terragrunt.hcl` - **with configuration for remote_state and AWS provider/**
    └── `common.terragrunt.hcl` - **defining common, project-specific variables**/
        └── `account.terragrunt.hcl` - **for each account/**
            └── `region.terragrunt.hcl` - **for each region within an account/**
                └── `env.terragrunt.hcl` - **for each environment within a region**

This allows flexible configuration, just add additional folders and adjust the configuration files, for instance configuring…

- Accounts `main` and `secondary`
- Regions `us-west-1` and `us-east-1` in `main` vs. `us-east-1` in `secondary`
- Environments `prod` in `main` regions vs. `stage` and `dev` in `secondary` regions