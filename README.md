# Terraform Interview Preparation

This repository contains resources, examples, and notes to help you prepare for a Terraform interview. It covers key Terraform concepts, commands, and best practices, along with examples to help you understand the declarative approach to infrastructure provisioning.

## Introduction

This repository is designed to help you understand Terraform from the ground up. It is structured to include both theory and practical examples, so you can get comfortable with how to use Terraform for provisioning and managing infrastructure.

## Core Terraform Concepts

### 1. **Providers**
   - What providers are in Terraform.
   - How to configure providers for different cloud platforms like AWS, Azure, and GCP.

### 2. **Resources**
   - What resources are and how to define them.
   - Example of a resource definition in Terraform.

### 3. **State Files**
   - The importance of the Terraform state file.
   - How Terraform tracks the infrastructure state.

### 4. **Variables and Outputs**
   - Using variables for dynamic configurations.
   - Using output values to display important information.

### 5. **Modules**
   - How to use modules for reusability and organization in Terraform configurations.

## Terraform Workflow

### 1. **terraform init**  
   Initializes the working directory for Terraform.

### 2. **terraform plan**  
   Generates an execution plan to show what changes Terraform will apply.

### 3. **terraform apply**  
   Applies the changes to your infrastructure.

### 4. **terraform destroy**  
   Destroys the infrastructure managed by Terraform.

### 5. **terraform validate**  
   Validates Terraform configuration files for errors.

### 6. **terraform fmt**  
   Formats the configuration files for consistency.

1. What is the difference between the declarative and imperative approaches in infrastructure management?

## Difference Between Declarative and Imperative Approaches in Infrastructure Management

### **Declarative Approach**:
In the **Declarative Approach**, you define **what** you want your infrastructure to look like, but you don't need to specify **how** to achieve that. The system (like Terraform) figures out the steps needed to create or manage the resources to match the desired state.

- **Example**: You define that you want an EC2 instance with a specific configuration (e.g., type, AMI), and Terraform will automatically create the instance for you.
- **How it works**: You describe the **end result** you want, and the system handles the process.
- **Advantages**: It’s easier to maintain and understand, especially when dealing with large and complex infrastructure. It also ensures that repeated actions lead to the same result.

#### Example (Terraform):
```hcl
resource "aws_instance" "example" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
}
```

## Imperative Approach in Infrastructure Management

### **What is the Imperative Approach?**
In the **Imperative Approach**, you tell the system **exactly how** to do something. You give step-by-step instructions on what actions need to be taken to create or manage your infrastructure.

### **How it Works:**
- You manually define **each step** needed to create or modify infrastructure.
- The system follows these steps in the order you’ve provided to reach the desired result.
- **Example**: If you want to create an EC2 instance, you would manually run a command for every action (e.g., creating the instance, configuring it, and updating it).

### **Example:**
Instead of saying “I want an EC2 instance,” you provide the detailed steps like:
1. Run a command to create an EC2 instance.
2. Run another command to update or configure the instance.

#### **Example with AWS CLI**:
```bash
# Step 1: Launch an EC2 instance with specific settings
aws ec2 run-instances --image-id ami-12345678 --instance-type t2.micro

# Step 2: Modify instance settings after launch
aws ec2 modify-instance-attribute --instance-id i-1234567890abcdef0 --no-disable-api-termination
```