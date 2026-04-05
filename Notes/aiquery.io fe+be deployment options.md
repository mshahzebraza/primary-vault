---
status: null
tags:
- architecture
- devops
- RnD
original_path: Notes/Work/aiquery.io/R&D/aiquery.io fe+be deployment options.md
base: Work
organization: '[[aiquery.io]]'
path_area: R&D
categories:
- '[[Work]]'
- '[[aiquery.io]]'
---

## Services Evaluated

1. Elastic Compute Service (ECS) on AWS
2. Serverless Architecture (AWS Lambda)
3. Auto-scaling Groups with EC2
4. AWS App Runner
5. AWS Elastic Beanstalk
6. ~~Kubernetes (EKS or Self-Managed)~~ — steep learning curve, complex config
7. ~~Hybrid Approaches (ECS + EKS + Lambda)~~ — too complicated

## Architecture Proposition 1 — ECS + EC2 (Public Subnet)

### Flow
```
VPC
└── Public Subnet
    └── ALB
    └── ECS (Autoscaling Group - EC2 instances)
        ├── Frontend Container
        └── Backend Container
```

### Cost Estimate
- ALB: ~USD 19.35/month (rough config — needs review)
- EC2 t3-medium (2 CPU, 4 GB) at 100% utilisation: ~USD 30.37/month
- VPC Interface Endpoint (frontend ↔ backend within VPC)
- Backend → MongoDB data transfer (1 TB/month):
  - via Internet: $90/month
  - via VPC Peering: ~$0 (should be free now)
  - via [PrivateLink](https://aws.amazon.com/blogs/apn/connecting-applications-securely-to-a-mongodb-atlas-data-plane-with-aws-privatelink/): ~$37/month (more secure, some processing included)
    - Interface Endpoint Fee: $7.2/connection/month
    - Data Processing: $10/TB
    - Data Transfer: $20/TB

## Architecture Proposition 2 — ECS + EC2 (Public + Private Subnet)

Components:
- ECR
- ECS (Tasks + Services)
- ALB
- EC2
- VPC
  - Public Subnet
  - Private Subnet

## Related Notes
- [[Accounts and Links]]
