# Terraform Interview Preparation

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
With Kubernetes, you describe the **desired state** of your application (e.g., the number of replicas of a pod, which container image to use, and how services should be exposed), and Kubernetes automatically ensures that the system matches this state.

### **How it Works:**
1. You write a YAML file that describes your application's resources (e.g., Deployment, Service).
2. You apply the YAML file using the `kubectl apply` command.
3. Kubernetes compares the current state with the desired state you defined.
4. If necessary, Kubernetes automatically takes action to ensure that the actual state matches your desired state (e.g., creating new pods or scaling up/down replicas).

### **Example: Kubernetes Declarative Configuration (YAML)**

Here’s an example of a declarative Kubernetes configuration file for a **Deployment** and a **Service**:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
  labels:
    app: my-app
spec:
  replicas: 3  # Defines the number of pod replicas
  selector:
    matchLabels:
      app: my-app  # Selector to match the app label in the pods
  template:
    metadata:
      labels:
        app: my-app  # Defines the label for the pod
    spec:
      containers:
      - name: my-app-container
        image: nginx:latest  # Container image to use
        ports:
        - containerPort: 80  # Port exposed by the container
---
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app  # Selects pods with the label 'app=my-app'
  ports:
    - protocol: TCP
      port: 80  # Port exposed by the service
      targetPort: 80  # Port exposed by the container in the pod
  type: LoadBalancer  # Exposes the service to the outside world
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
## Key Differences Between Declarative and Imperative Approaches

| **Aspect**                | **Declarative Approach**                                                   | **Imperative Approach**                                                   |
|---------------------------|----------------------------------------------------------------------------|----------------------------------------------------------------------------|
| **What You Define**        | You define **what** you want (desired state) and let the system figure out **how** to achieve it. | You define **how** to achieve the result, specifying each step of the process. |
| **System Behavior**        | The system manages and adjusts to achieve the desired state automatically. | The system follows your exact instructions without automatic adjustments.  |
| **Control Over Process**   | Less control over the specific steps. You focus on the end result.         | Full control over each step and action in the process.                    |
| **Ease of Maintenance**    | Easier to maintain; just update the desired state and apply it again.      | Harder to maintain, especially with complex systems. Requires manual updates for each change. |
| **Idempotency**            | **Idempotent**: Re-running the same configuration results in the same outcome. | Not necessarily idempotent; re-running may create duplicate resources or repeat steps. |
| **Focus**                  | Focuses on the **desired end state** (e.g., number of replicas, container image). | Focuses on the **process** and **steps** needed to achieve the goal.      |

### **Summary**:
- **Declarative**: You describe **what** you want (e.g., desired state) and the system takes care of the rest.
- **Imperative**: You define **how** to achieve the goal, step-by-step.


