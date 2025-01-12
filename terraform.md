# Terraform Installation and Configuration

To gain an understanding of Terraform's overview and folder structure, please refer to the `README.md` file.


# Terraform Installation 

## Installation:

Install Terraform Binary --> Configure the environment variable.
Install VS code --> Install Hashi Corp Extension.


### Authentication & Authorization:

We have different providers like `Aws, GCP, Azure, Kubernetes, GitHub`. So, for terraform to connect to these providers, it needs authentication. Also to do any operation within these providers it needs authorization.

### For ex:

Let’s Consider Aws Provider. Here terraform to connect to aws, we need to create an IAM user. 

### For Ex: 

IAM User: John, IAM policy:  Nil    -->   Generate Access Key and Secret Key 

Now in your local machine terminal run aws configure command and provide the access and secret key of IAM user john.


Create a simple terraform code to create s3 bucket. The terraform script will get failed, as because the IAM user can have permission to login to the aws account but have no permission to create resource inside the aws account.

IAM User: Naveen, IAM policy:  s3 bucket access with write permission -->   Generate Access Key and Secret Key.
Now in your local machine terminal run aws configure command and provide the access and secret key of IAM user Naveen.


Create a simple terraform code to create s3 bucket. The terraform script will now create s3 bucket. But if we tried to create any other resource such as ec2, vpc. It will gets fail as because IAM user Naveen have only s3 bucket access.

### Note:

Whenever you create terraform, code make sure that to provide least level of access for the IAM User.



### Images:

![Access credentials ](./images/Access%20credentials%20overview.png)


### Note:

In the below, you can able to see that instead of storing access and secret keys in your terminal using aws configure command, we can also pass it directly in terraform provider code.

```
// Provider.tf


provider "aws" {
  region     = "us-west-2"
  access_key = "my-access-key"
  secret_key = "my-secret-key"
}

```


### Note:

For terraform, we can create an IAM user with name `terraform` and then we can assign IAM policy for that.

Ec2 Instance creation using terraform:

Go to terraform official document --> Search `terraform aws document` in browser


![ec2 image ](./images/ec2%20image.png)



![ec2 image ](./images/ec2%20image1.png)



So, it is always good practice to check the argument reference in terraform document while creating terraform code for each resource.



## Terraform Commands:

1. terraform init  --> Initialize the terraform (It will create .terraform folder (inside this folder it automatically downloads the plugin required for the provider and module) and .terraform.lock.hcl file, which contains provider & module version and other details related to it.)

2. terraform fmt  --> to format the terraform (correct the indentation of terraform code).

3. terraform validate -->

4. terraform plan --> 

5. terraform apply -->

6. terraform apply –auto-approve -->

7. terraform destroy -->

8. terraform destroy –auto-approve -->


## Note:

In production, before running terraform apply always run terraform plan and check what all the resource it is going to create and the other detail.

Then instead of running `terraform apply –auto-approve`, in production run `terraform apply` this will ask for the approval in terminal. Also, it will show `+` or `–` of the resource. Suppose if a resource is going to get created means it will show `+ aws_ec2` (or) if a tag is added in ec2 means `+ tags in aws_ec2`.



## Terraform Provider:


![Terraform provider ](./images/Terraform%20provider.png)



![Terraform provider1 ](./images/Terraform%20provider1.png)


It is standard practice to use `required_providers`.  Using this we can also configure the `version` of provider, provider namespace such as `HashiCorp/aws, HashiCorp/azure` etc.