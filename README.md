# AWS DevOps Platform - Advanced Bootcamp

A comprehensive DevOps bootcamp covering AWS infrastructure, Kubernetes, CI/CD, observability, and security best practices.

## Overview

This repository contains practical implementations of AWS DevOps patterns, following the AWS Well-Architected Framework. Each day focuses on specific technologies and patterns, building up to a complete production-ready platform.

## Bootcamp Days

### Foundation Phase
- [**Day 0**](./docs/advanced-bootcamp/00-day/README.md) - Repository planning, architecture definition, and cost awareness
- [**Day 1**](./docs/advanced-bootcamp/01-day/README.md) - EKS & GitHub Actions setup
- [**Day 2**](./docs/advanced-bootcamp/02-day/README.md) - Terraform: VPC, IAM, RDS, S3
- [**Day 3**](./docs/advanced-bootcamp/03-day/README.md) - Core AWS Services: EC2, Aurora MySQL, OpenSearch, Redis

### Application Deployment Phase
- [**Day 4**](./docs/advanced-bootcamp/04-day/README.md) - App via Helm (Laravel example)
- [**Day 5**](./docs/advanced-bootcamp/05-day/README.md) - Observability: Fluentd + OpenSearch + Grafana
- [**Day 6**](./docs/advanced-bootcamp/06-day/README.md) - Frontend: S3 + CloudFront
- [**Day 7**](./docs/advanced-bootcamp/07-day/README.md) - Quality & Security: SonarQube, Trivy, PHPStan, Parameter Store

### CI/CD & Infrastructure Phase
- [**Day 8**](./docs/advanced-bootcamp/08-day/README.md) - CI/CD Infra: Terraform for S3 + IAM for pipelines

### Kubernetes Challenge Series
- [**Day 9**](./docs/advanced-bootcamp/09-day/README.md) - AWS EKS Kubernetes Challenge Series
- [**Day 10**](./docs/advanced-bootcamp/10-day/README.md) - Kubernetes Basics: Deployments and Services on EKS
- [**Day 11**](./docs/advanced-bootcamp/11-day/README.md) - Infrastructure as Code: Terraforming Kubernetes Resources
- [**Day 12**](./docs/advanced-bootcamp/12-day/README.md) - IAM Roles and Service Accounts: EKS Security Integration

## Remember
### Tags

All resources are tagged consistently:

| Key | Value |
|-----|-------|
| Project | aw-bootcamp |
| Environment | sandbox/dev |
| ManagedBy | Terraform |

## Destroy Policy

> [!WARNING]
> Always destroy sandbox resources after use.
> 
> **Rules:**
> - Sandbox infrastructure is temporary
> - No long-lived resources are allowed
> - Terraform `destroy` is mandatory after each exercise

## Cost Optimization

This bootcamp is designed with cost optimization in mind:
- Uses AWS free tier where possible
- Implements resource tagging for cost tracking
- Uses spot instances and right-sized resources
- Includes cleanup scripts for all resources

## Security Best Practices

Following the AWS Well-Architected Framework Security Pillar:
- Least-privilege IAM policies
- Secrets management with AWS SSM Parameter Store
- Container scanning with Trivy
- OIDC-based authentication for GitHub Actions
- IRSA (IAM Roles for Service Accounts) for EKS
