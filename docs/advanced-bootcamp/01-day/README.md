# Day 1 – EKS & GitHub Actions

## Todo
- [x] Configure AWS account  
  - [ ] Create IAM user `aw-bootcamp` with minimum policies  
  - [x] Configure AWS CLI with a new profile `--profile aw-bootcamp`  
- [x] Create EKS cluster with `eksctl` – [installation](https://github.com/eksctl-io/eksctl)  
- [x] Add a [Dockerfile](/app/Dockerfile) to host an Apache web server  
  - [ ] Create ECR repository  
    - [x] Add GitHub Actions  
      - [x] Add IAM roles to give access to GitHub Actions within my repository  
- [x] Create Terraform to replicate the `eksctl` task  
- [ ] Add GitHub Action to automate Kubernetes manifests  

---

## 1. Configure AWS account

> [!INFO]  
> Based on the AWS Well-Architected Framework – Security Pillar:  
> We must grant only the **least-privilege access** when provisioning specific resources.  
> In this case, access is limited to administering services within AWS.  
>  
> - [SEC03-BP02: Grant least-privilege access](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_permissions_least_privileges.html)

- I wanted to create a specific IAM user with minimum access for today’s use cases.  
  - I wasn’t sure if I had enough permissions to do it, so I didn’t accomplish this step.  
- Later, in the problem cases, I created a role to give **AmazonEC2ContainerRegistryPowerUser** access for ECR usage.  
- Then, I added a specific policy for `eks:DescribeCluster` to allow querying the EKS cluster.  

---

## 2. EKS cluster creation using `eksctl`

I tried the `eksctl` CLI to create the cluster, testing the simplicity of this tool.

- Installation: https://github.com/eksctl-io/eksctl  

---

## 3. Dockerfile and GitHub Actions

- [Dockerfile: Apache web server](/app/Dockerfile)  
- [GitHub Action to use ECR: `.github/workflows/ci.yaml`](/.github/workflows/ci.yaml)  

> [!INFO]  
> I created an IAM role to provide limited but necessary action policies to my repository,  
> allowing GitHub runners to authenticate using a simpler and more secure approach.

### AmazonEC2ContainerRegistryPowerUser
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ecr:GetAuthorizationToken",
        "ecr:BatchCheckLayerAvailability",
        "ecr:GetDownloadUrlForLayer",
        "ecr:GetRepositoryPolicy",
        "ecr:DescribeRepositories",
        "ecr:ListImages",
        "ecr:DescribeImages",
        "ecr:BatchGetImage",
        "ecr:GetLifecyclePolicy",
        "ecr:GetLifecyclePolicyPreview",
        "ecr:ListTagsForResource",
        "ecr:DescribeImageScanFindings",
        "ecr:InitiateLayerUpload",
        "ecr:UploadLayerPart",
        "ecr:CompleteLayerUpload",
        "ecr:PutImage"
      ],
      "Resource": "*"
    }
  ]
}
```

### Specific Inline Policy
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "VisualEditor0",
      "Effect": "Allow",
      "Action": "eks:DescribeCluster",
      "Resource": "arn:aws:eks:us-east-1:711387135481:cluster/aw-bootcamp-cluster"
    }
  ]
}
```

---

## 4. Optional: Terraform

You can find the Terraform implementation in `/infra/terraform`.

- Separation of modules  
- Implementation of variables and outputs for better management  

---

## Kubernetes Manifests and Deployment

- Deployment workflow:  
  - [.github/workflows/ci.yaml](/.github/workflows/ci.yaml)  
- Kubernetes manifests:  
  - [k8s/manifests/deployment.yaml](/k8s/manifests/deployment.yaml)  
  - [k8s/manifests/service.yaml](/k8s/manifests/service.yaml)  
