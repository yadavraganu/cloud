## **What is Amazon VPC?**

Amazon VPC is a **logically isolated network** within the AWS cloud where you can launch AWS resources (like EC2 instances). It gives you full control over your virtual networking environment, including IP address ranges, subnets, route tables, gateways, and security settings.

### **Core Concepts of VPC**

### 1. **CIDR Block**
- Defines the IP address range of your VPC.
- Example: `10.0.0.0/16` gives you 65,536 IP addresses.

### 2. **Subnets**
- Divide your VPC into smaller networks.
- **Public Subnet**: Connected to the internet via an Internet Gateway.
- **Private Subnet**: No direct internet access.

### 3. **Internet Gateway (IGW)**
- A horizontally scaled, redundant, and highly available VPC component.
- Enables communication between instances in your VPC and the internet.

### 4. **NAT Gateway**
- Allows instances in a private subnet to access the internet **without** exposing them to incoming traffic.

### 5. **Route Tables**
- Control traffic routing within your VPC.
- Each subnet must be associated with a route table.

### 6. **Security Groups**
- Virtual firewalls for EC2 instances.
- Stateful: return traffic is automatically allowed.

### 7. **Network ACLs (Access Control Lists)**
- Stateless firewalls at the subnet level.
- You must define both inbound and outbound rules.

### 8. **VPC Peering**
- Connects two VPCs privately.
- Useful for cross-account or cross-region communication.

### 9. **AWS Transit Gateway**
- A hub that connects multiple VPCs and on-prem networks.

### 10. **VPC Endpoints**
- Private connections to AWS services without using the internet.
- Types: **Interface Endpoint** and **Gateway Endpoint**.

## What Are Security Groups in AWS?

**Security Groups** are virtual firewalls that control **inbound and outbound traffic** to AWS resources—primarily **EC2 instances**. They operate at the **instance level**, not the subnet level.

### Key Characteristics

- **Stateful**: If you allow inbound traffic, the response is automatically allowed outbound.
- **Instance-Level**: Applied directly to EC2 instances or other supported resources.
- **Allow Rules Only**: You can only specify what traffic is allowed; all other traffic is implicitly denied.
- **Multiple Groups**: You can assign multiple security groups to a single instance.

### 📥 Inbound Rules

Define what traffic is **allowed to reach** your instance.

Example:
- Allow SSH from your IP: `TCP port 22` from `203.0.113.0/32`
- Allow HTTP from anywhere: `TCP port 80` from `0.0.0.0/0`

### 📤 Outbound Rules

Define what traffic your instance is **allowed to send out**.

Example:
- Allow all outbound traffic: `0.0.0.0/0` on all ports (default)

### Where to Use Security Groups

| Resource Type        | Use Case Example                                      |
|----------------------|--------------------------------------------------------|
| **EC2 Instances**     | Control access via SSH, HTTP, HTTPS, etc.             |
| **RDS Databases**     | Allow access only from specific EC2 or IP ranges      |
| **Elastic Load Balancers** | Define allowed traffic to backend instances         |
| **Lambda (VPC-enabled)** | Control access to other VPC resources               |
| **ECS Tasks (Fargate)** | Secure communication between containers              |
