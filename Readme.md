# AWS Terraform Modules

This repository contains information and documentation related to AWS Terraform modules. Each module will have a dedicated folder, which includes a `README.md` file for detailed documentation.

## Standard Practices

We adhere to standard best practices for creating AWS Terraform modules. The modules are designed to be loosely coupled, enabling their use in various use cases. 

## Key Features of the Modules

1. Modular and reusable design.
2. Use of Terraform functions such as `for each`, `count`, `when`, `local`, `data`, etc.
3. Flexibility to adapt to diverse use cases and requirements.

By following these principles, the modules ensure maintainability, scalability, and ease of integration into different projects.


# Folder Structure of Terraform used in production

In a production environment, having a well-organized Terraform folder structure is crucial for maintainability, scalability, and collaboration among teams. A common approach is to structure Terraform configurations to separate different environments, modularize components, and define clear workflows for infrastructure changes.


## 1. Root Directory


The root directory contains global configurations, environment directories, and any general documentation or scripts.


### Images:

![Root Directory Logo](./images/Terraform%20folder%20structure%20root%20directory.png)



## 2. Detailed Folder Breakdown


### 2.1. environments/ Directory


This folder contains configurations for different environments `(e.g., dev, staging, prod)`. Each environment has its own state and variables to isolate resources.


### Images:

![environments Directory Logo](./images/Terraform%20folder%20structure%20environment%20directory.png)




Key Components:

1. main.tf: Defines resources and infrastructure for the environment.
2. variables.tf: Specifies input variables.
3. outputs.tf: Declares outputs for the environment.
4. terraform.tfvars: Environment-specific variable values (e.g., region, instance size).
5. backend.tf: Configures remote state storage (e.g., S3, Azure Blob, etc.).


### 2.2. modules/ Directory


Modules represent reusable components (e.g., VPC, ECS, RDS, IAM) and are stored in the modules/ directory. Each module has its own folder.


### Images:

![modules Directory Logo](./images/Terraform%20folder%20structure%20modules%20directory.png)



Key Benefits of Modules:

1. Promotes reusability.
2. Simplifies infrastructure management.
3. Encourages best practices across environments.



### 2.3. scripts/ Directory


This folder contains helper scripts for tasks like initializing Terraform, managing remote state, or deploying changes.


### Images:


![scripts Directory Logo](./images/Terraform%20folder%20structure%20scripts%20directory.png)



Use Case: Centralized scripts reduce human error and streamline workflows.




### 2.4. Root-Level Configuration Files


At the root of the project, you define global configurations applicable to all environments.

1. `main.tf`: A high-level entry point for global resources (if applicable).
2. `variables.tf`: Global variables used across environments.
3. `outputs.tf`: Global outputs for cross-environment dependencies.
4. `provider.tf`: Configures the cloud provider (e.g., AWS, Azure, GCP).
5. `terraform.tfvars`: Default variable values for all environments.
6. `README.md`: Documentation for the Terraform project.





## 3. Example Full Folder Structure


### Images:


![Full Folder Directory Structure](./images/Terraform%20full%20folder%20structure.png)



## 4. Additional Best Practices

1. Use `Remote State`: Store state files in a secure remote backend like AWS S3, Azure Blob, or GCP Buckets.

2 Use `Workspaces`: Separate state management for environments (if environments are not in folders).

3. `Version Control`: Store the entire Terraform directory in a Git repository for versioning and collaboration.

4. `Environment-Specific Overrides`: Keep sensitive information in environment-specific .tfvars files and secure them using tools like HashiCorp Vault or AWS Secrets Manager.

5. `Linting and Validation`: Use tools like terraform fmt, terraform validate, and tflint for consistent and error-free configurations.
Automation: Integrate Terraform workflows with `CI/CD pipelines` for consistent deployments.

6. By following this structure, your Terraform project remains modular, maintainable, and suitable for scaling in production environments.


# When to use Root Level Directory and when to skip Root Level Directory

The best practice is to combine both approaches: use a root folder for shared infrastructure and a separate environments folder for environment-specific configurations. This allows you to manage global resources in one place while maintaining the flexibility to customize settings for each environment.


## when to skip Root Level Directory

If each environment operates independently with no shared resources or configurations, you don't need a `root-level` main.tf. Instead, keep all configurations self-contained within environment folders.

### Images:


![Skip root folder Structure](./images/skip%20root%20folder.png)

Here, each environment is treated as an independent Terraform configuration, and the root folder is just a container for organization.

### Best Practices

1. Use a root-level main.tf:

* When you have shared resources or modules.
* For centralized management or global configurations.
* To define Terraform backends or workspaces.

2. Avoid a root-level main.tf:

* When environments are completely isolated and independent.
* When environment-specific configurations don't need to reference shared resources.

3. Ensure modularity:

* Use modules for reusable components, whether at the root level or environment-specific levels.

By understanding your use case (shared vs. independent), you can decide whether a root-level main.tf is necessary.


# Let's Consider an Example when to use root folder vs when to skip root folder:


## 1. when to skip root folder  --> Independent Resource

If each environment operates independently with no shared resources or configurations, you don't need a root-level main.tf. Instead, keep all configurations self-contained within environment folders.

### Images:


![Skip root folder Structure](./images/skip%20root%20folder.png)

## 2. when to use root folder  --> Shared Resource

### Scenario: Multiple Environments (dev, prod) with Shared Resources

We have two environments: `dev and prod`. Both environments need to use an S3 bucket, but the dev and prod environments have different configurations.

We also have some `shared resources` like a VPC and IAM roles that are common to both environments.


### Folder Structure


### Images:


![Shared folder Structure](./images/Shared%20folder%20Structure.png)


### Explanation

1. Root-Level main.tf (Shared Resources):

* The root-level main.tf is used to define shared resources like VPC, IAM roles, or modules that are used across both dev and prod environments.
* You can also configure the backend here if you're using a shared state.

2. Environment-Specific main.tf:

* Each environment (e.g., dev, prod) has its own main.tf file where you specify the environment-specific configurations like the S3 bucket name, versioning, etc.
* These files will reference the modules defined in the root or shared resources.


## Terraform Installation and Configuration

For detailed instructions on installing Terraform and configuring it for use, please refer to the `terraform.md` file included in this repository.


## Terraform Standards

For detailed instructions on Terraform Standards, please refer to the `terraform_standards.md` file included in this repository.

