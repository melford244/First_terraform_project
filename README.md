# Automated EC2 Instance Deployment on AWS Using Terraform: A Step-by-Step Guide
Here’s a step-by-step guide to launch an EC2 instance using Terraform and retrieve the instance ID using Terraform commands (init, plan, apply, and destroy). This guide assumes you have Terraform installed and AWS credentials configured.

## Architecture Diagram

![Image Alt](https://raw.githubusercontent.com/melford244/First_terraform_project/3cc8a7116ddf39247eb75ddbc88ac2c0ce3c4886/terraform.drawio.png)

# Detailed Steps 
Step 1: Set Up Your Terraform Configuration File
Create a directory for your Terraform project:

bash
Copy
mkdir terraform-ec2
cd terraform-ec2
Create a Terraform configuration file named main.tf:

hcl
Copy
provider "aws" {
  region = "us-east-1"  # Replace with your preferred AWS region
}

resource "aws_instance" "example" {
  ami           = "ami-0c02fb55956c7d316"  # Replace with a valid AMI ID for your region
  instance_type = "t2.micro"              # Replace with your desired instance type

  tags = {
    Name = "example-instance"
  }
}

output "instance_id" {
  description = "The ID of the EC2 instance"
  value       = aws_instance.example.id
}
Replace the ami value with a valid AMI ID for your region (e.g., Amazon Linux 2 AMI).

Replace the instance_type if needed (e.g., t3.micro).

Step 2: Initialize Terraform
Run the terraform init command to initialize the working directory and download the necessary provider plugins:

bash
Copy
terraform init
Output Example:

Copy
Terraform has been successfully initialized!
Step 3: Review the Execution Plan
Run the terraform plan command to see what Terraform will do before applying the changes:

bash
Copy
terraform plan
Output Example:

Copy
Plan: 1 to add, 0 to change, 0 to destroy.
This shows that Terraform will create 1 resource (the EC2 instance).

Step 4: Apply the Configuration
Run the terraform apply command to create the EC2 instance:

bash
Copy
terraform apply
Terraform will show the execution plan again and ask for confirmation. Type yes to proceed.

Output Example:

Copy
Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

Outputs:

instance_id = "i-0abcd1234efgh5678"
The instance_id output will display the ID of the newly created EC2 instance.

Step 5: Verify the EC2 Instance
Log in to the AWS Management Console.

Navigate to EC2 > Instances.

Verify that the instance with the ID i-0abcd1234efgh5678 (or similar) is running.

Step 6: Destroy the Resources (Optional)
To clean up and delete the EC2 instance, run the terraform destroy command:

bash
Copy
terraform destroy
Terraform will show the resources it plans to destroy and ask for confirmation. Type yes to proceed.

Output Example:

Copy
Destroy complete! Resources: 1 destroyed.
Summary of Commands:
Initialize Terraform:

bash
Copy
terraform init
Review the Plan:

bash
Copy
terraform plan
Apply the Configuration:

bash
Copy
terraform apply
Destroy the Resources:

bash
Copy
terraform destroy
