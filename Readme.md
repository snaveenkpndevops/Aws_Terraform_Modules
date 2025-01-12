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



