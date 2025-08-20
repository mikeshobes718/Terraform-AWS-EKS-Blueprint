# Terraform-AWS-EKS-Blueprint

A blueprint for deploying a production-grade EKS cluster on AWS using Terraform.

## 🏗️ Project Overview

This project demonstrates **Infrastructure as Code (IaC)** best practices for deploying a production-ready Amazon EKS (Elastic Kubernetes Service) cluster on AWS. Built with Terraform, it showcases enterprise-level infrastructure design that a Senior DevOps Engineer would deploy in production environments.

## 🎯 What This Project Delivers

- **Complete EKS Infrastructure**: VPC, subnets, IAM roles, and EKS cluster
- **Production-Ready Design**: Multi-AZ deployment with proper networking
- **Security Best Practices**: Private subnets, IAM roles with least privilege
- **Professional Documentation**: Comprehensive README with architecture diagrams
- **Git Best Practices**: Proper commit history and version control

## 🏛️ Architecture Diagram

```
AWS EKS Infrastructure Architecture
====================================

                    Internet
                       │
                       ▼
              ┌─────────────────┐
              │ Internet Gateway│
              └─────────────────┘
                       │
                       ▼
              ┌─────────────────┐
              │      VPC        │
              │  10.0.0.0/16   │
              └─────────────────┘
                       │
                       ▼
        ┌─────────────────────────────────┐
        │                                 │
        ▼                                 ▼
┌─────────────┐                   ┌─────────────┐
│Availability │                   │Availability │
│   Zone A    │                   │   Zone B    │
│ (us-east-1a)│                   │ (us-east-1b)│
└─────────────┘                   └─────────────┘
        │                                 │
        ▼                                 ▼
┌─────────────┐                   ┌─────────────┐
│Public Subnet│                   │Public Subnet│
│ 10.0.1.0/24│                   │ 10.0.2.0/24│
│   Route    │                   │   Route    │
│  Table     │                   │  Table     │
└─────────────┘                   └─────────────┘
        │                                 │
        ▼                                 ▼
┌─────────────┐                   ┌─────────────┐
│Private      │                   │Private      │
│Subnet       │                   │Subnet       │
│10.0.3.0/24 │                   │10.0.4.0/24 │
│             │                   │             │
│┌───────────┐│                   │┌───────────┐│
││EKS Worker ││                   ││EKS Worker ││
││  Node 1   ││                   ││  Node 2   ││
│└───────────┘│                   │└───────────┘│
└─────────────┘                   └─────────────┘
        │                                 │
        └─────────────┬───────────────────┘
                      │
                      ▼
              ┌─────────────────┐
              │   EKS Cluster   │
              │ Control Plane   │
              │ (Managed by AWS)│
              └─────────────────┘
```

**Key Components:**
- **VPC**: Virtual Private Cloud with CIDR 10.0.0.0/16
- **Public Subnets**: For load balancers and internet access
- **Private Subnets**: For EKS worker nodes (more secure)
- **Internet Gateway**: Provides internet access to public subnets
- **Route Tables**: Control traffic flow between subnets
- **EKS Cluster**: Kubernetes control plane managed by AWS
- **Worker Nodes**: Run your application containers

**Security Features:**
- Private subnets for worker nodes
- IAM roles with least privilege access
- Security groups automatically managed by EKS
- Network ACLs for additional security layers

## 🚀 Quick Start

### Prerequisites
- AWS CLI configured with appropriate credentials
- Terraform installed (version 1.5.7 or later)
- Git for version control

### Deployment Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/mikeshobes718/Terraform-AWS-EKS-Blueprint.git
   cd Terraform-AWS-EKS-Blueprint
   ```

2. **Initialize Terraform**
   ```bash
   terraform init
   ```

3. **Review the Plan**
   ```bash
   terraform plan
   ```

4. **Deploy Infrastructure**
   ```bash
   terraform apply -auto-approve
   ```

5. **Clean Up (When Done)**
   ```bash
   terraform destroy -auto-approve
   ```

## 📁 Project Structure

```
├── README.md              # Project documentation
├── variables.tf           # Input variables (AWS region)
├── main.tf               # Main infrastructure code
├── outputs.tf            # Output values
├── .terraform.lock.hcl   # Provider version lock file
└── .gitignore            # Git ignore patterns
```

## 🔧 Configuration

### Variables
- **`aws_region`**: AWS region for deployment (default: us-east-1)

### Infrastructure Details
- **EKS Version**: 1.28
- **Node Group**: Auto-scaling (1-4 nodes)
- **Instance Type**: t3.small (Free Tier compatible)
- **VPC CIDR**: 10.0.0.0/16
- **Subnets**: 4 subnets across 2 availability zones

## 🛡️ Security Features

- **Network Security**: Private subnets for worker nodes
- **IAM Security**: Least privilege access with proper role separation
- **Encryption**: EBS encryption and TLS for API communication
- **Access Control**: Public/private API endpoints with security groups

## 💰 Cost Optimization

- **Free Tier Compatible**: Uses t3.small instances
- **Auto-scaling**: Scales nodes based on demand
- **Resource Tagging**: Proper tagging for cost tracking
- **Cleanup**: Easy destruction to avoid ongoing charges

## 🧪 Testing & Validation

### Terraform Commands
```bash
# Validate configuration
terraform validate

# Check formatting
terraform fmt

# Plan deployment
terraform plan

# Apply changes
terraform apply

# Destroy infrastructure
terraform destroy
```

### AWS Verification
- Verify VPC creation in AWS Console
- Check EKS cluster status
- Validate subnet configurations
- Confirm IAM roles and policies

## 🚨 Important Notes

- **Cost Awareness**: This infrastructure will incur AWS charges
- **Cleanup Required**: Always run `terraform destroy` when done
- **Production Use**: Modify configurations for production environments
- **Security Review**: Review IAM policies before production deployment

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📚 Learning Resources

- [Terraform Documentation](https://www.terraform.io/docs)
- [AWS EKS Documentation](https://docs.aws.amazon.com/eks/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/)

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- HashiCorp for Terraform
- AWS for EKS service
- Kubernetes community
- DevOps best practices community

---

**Built with ❤️ for learning and professional development**
