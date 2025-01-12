# Terraform Standard Notes:

1. For each variable, please comment the purpose of that variable.
2. For Sensitive value, use sensitive variable in `input.tf` file.
3. Don't directly store secrets as variable in `input.tf` as a default value.
4. Use default value in variable in `input.tf` .
5. Configure variable type such as `string, bool` in `input.tf` .
6. Include tags in all resource. Tags include `environment, owner, project, and other relevant metadata`.
7. Standarized Resource Naming 

	* The pattern <project>-<environment>-<resource> can be applied like this:
	
	Ex: banking-prod-vm,
        banking-dev-vm,
        banking-qa-vm      
		
	Here banking is the project, prod is the environment, vm is the resource.
	
8. Create a separate file for provider like `provider.tf`. provider version is important. Ensure that each environment (prod, dev, staging) has its own provider configuration. This avoids cross-environment contamination and maintains clear boundaries between environments. 

9. It is always good to use `with required_providers` for configuring providers.

	```
    terraform { 
	  required_providers {
		aws = {
		  source  = "hashicorp/aws"
		  version = "~> 5.0"
		}
	  }
	}

	provider "aws" {
	  region = "us-east-1"
	}

    ```
	
	purpose: Terraform Version will be same in all members machine, also it will be same in all environment.
	
	
	Note:
	
	In projects with multiple providers (e.g., AWS, Azure, Kubernetes), explicitly declaring providers with required_providers ensures all dependencies are clear and unambiguous.

    ```
	
	terraform {
	  required_providers {
		aws = {
		  source  = "hashicorp/aws"
		  version = "~> 5.0"
		}
		azurerm = {
		  source  = "hashicorp/azurerm"
		  version = "~> 3.0"
		}
	  }
	}

	provider "aws" {
	  region = "us-east-1"
	}

	provider "azurerm" {
	  features {}
	}


    ```

	
	---
	
	`without required_providers`
	
    ```
	provider "aws" {
        region = "us-east-1"
    }

    ```

10. Use `terraform.tfvars` for configuring the variable. Use separate `.tfvars` files for different environments (e.g., dev.tfvars, prod.tfvars). 

11. Create Inline comment for each resource like below:

	```
	  resource "aws_instance" "example" {
        ami           = "ami-0c55b159cbfafe1f0" # Amazon Linux 2 AMI (specific for us-east-1)
        instance_type = "t2.micro"              # Small instance type suitable for testing
        tags = {
            Name = "ExampleInstance"             # Tag to identify the instance in AWS
        }
	}

	
	```
	
12. Create `Readme.md` for each module. [describes the purpose, usage, inputs, outputs, and any dependencies or requirements. ]

13. Versioning Documentation: Clearly document the versioning of modules and terraform itself. Ensure that readers understand which versions of Terraform and providers the code is compatible with. 

14. `Terraform fmt`: Always run terraform fmt before committing code to ensure consistent formatting.

    `Linting Tools`: Use Terraform linting tools such as tflint to catch common mistakes and enforce best practices. 

	`Pre-Commit Hooks`: Implement pre-commit hooks to automate formatting and linting checks before code is committed. 
	
	
15. Store secrets in Aws secret manager etc. implement strict access control with least privilege.

16. Store `terraform.tfstate` file in s3 with server side encryption, along with locking mechanism. Also have a `terraform.tfstate` file backup. for this in s3 bucket enable versioning is the best approach. 

17. teraform validate, terraform plan. Also integrate terraform with CI/CD.

18. Use separate branch in github to maintain terraform code. use PR for code review. Commit message should be standard and clear. Always commit the .terraform.lock.hcl file to version control to ensure consistency in provider versions across environments.

19. Terraform taint --> explore this ?  [Resource Re-creation with Tainting ]

### Note:

Check what is terraform lint, terraform taint?