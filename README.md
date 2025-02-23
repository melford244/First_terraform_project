# Automated EC2 Instance Deployment on AWS Using Terraform: A Step-by-Step Guide
Here’s a step-by-step guide to launch an EC2 instance using Terraform and retrieve the instance ID using Terraform commands (init, plan, apply, and destroy). This guide assumes you have Terraform installed and AWS credentials configured.

### **Precaution**
- **AWS Credentials:** Ensure your AWS credentials are configured. You can use the `~/.aws/credentials` file or environment variables (`AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`).
- **AMI ID:** Use the correct AMI ID for your region. You can find AMI IDs in the AWS Management Console or using the AWS CLI:
  ```bash
  aws ec2 describe-images --owners amazon --filters "Name=name,Values=amzn2-ami-hvm-*" --query "Images[*].[ImageId,Name]" --output table
  ```

## Architecture Diagram
![Image Alt](https://raw.githubusercontent.com/melford244/First_terraform_project/3cc8a7116ddf39247eb75ddbc88ac2c0ce3c4886/terraform.drawio.png)

# Detailed Steps 
(Due to technical issues, the search service is temporarily unavailable.)

Here’s a **step-by-step guide** to launch an EC2 instance using Terraform and retrieve the instance ID using Terraform commands (`init`, `plan`, `apply`, and `destroy`). This guide assumes you have Terraform installed and AWS credentials configured.

---

### **Step 1: Set Up Your Terraform Configuration File**
1. Create a directory for your Terraform project:
   ```bash
   mkdir terraform-ec2
   cd terraform-ec2
   ```

2. Create a Terraform configuration file named `main.tf`:
   ```hcl
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
   ```

   - Replace the `ami` value with a valid AMI ID for your region (e.g., Amazon Linux 2 AMI).
   - Replace the `instance_type` if needed (e.g., `t3.micro`).

---

### **Step 2: Initialize Terraform**
1. Run the `terraform init` command to initialize the working directory and download the necessary provider plugins:
   ```bash
   terraform init
   ```

   **Output Example:**
   ```
   Terraform has been successfully initialized!
   ```

---

### **Step 3: Review the Execution Plan**
1. Run the `terraform plan` command to see what Terraform will do before applying the changes:
   ```bash
   terraform plan
   ```

   **Output Example:**
   ```
   Plan: 1 to add, 0 to change, 0 to destroy.
   ```

   - This shows that Terraform will create 1 resource (the EC2 instance).

---

### **Step 4: Apply the Configuration**
1. Run the `terraform apply` command to create the EC2 instance:
   ```bash
   terraform apply
   ```

2. Terraform will show the execution plan again and ask for confirmation. Type `yes` to proceed.

   **Output Example:**
   ```
   Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

   Outputs:

   instance_id = "i-0abcd1234efgh5678"
   ```

   - The `instance_id` output will display the ID of the newly created EC2 instance.

---

### **Step 5: Verify the EC2 Instance**
1. Log in to the **AWS Management Console**.
2. Navigate to **EC2 > Instances**.
3. Verify that the instance with the ID `i-0abcd1234efgh5678` (or similar) is running.

---

### **Step 6: Destroy the Resources (Optional)**
1. To clean up and delete the EC2 instance, run the `terraform destroy` command:
   ```bash
   terraform destroy
   ```

2. Terraform will show the resources it plans to destroy and ask for confirmation. Type `yes` to proceed.

   **Output Example:**
   ```
   Destroy complete! Resources: 1 destroyed.
   ```

---

### **Summary of Commands:**
1. **Initialize Terraform:**
   ```bash
   terraform init
   ```

2. **Review the Plan:**
   ```bash
   terraform plan
   ```

3. **Apply the Configuration:**
   ```bash
   terraform apply
   ```

4. **Destroy the Resources:**
   ```bash
   terraform destroy
   ```

---

