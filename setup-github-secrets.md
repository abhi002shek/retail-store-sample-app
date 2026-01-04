# GitHub Secrets Setup

## Required Secrets

Go to your GitHub repository → **Settings** → **Secrets and variables** → **Actions**

Add these repository secrets:

| Secret Name             | Description                    | How to Get                           |
|------------------------|--------------------------------|--------------------------------------|
| `AWS_ACCESS_KEY_ID`    | AWS Access Key                 | `aws configure list`                 |
| `AWS_SECRET_ACCESS_KEY`| AWS Secret Access Key          | From AWS IAM user credentials        |
| `AWS_REGION`           | AWS Region                     | `us-west-2` (or your preferred)      |
| `AWS_ACCOUNT_ID`       | AWS Account ID                 | `aws sts get-caller-identity --query Account --output text` |

## Quick Commands to Get Values

```bash
# Get AWS Account ID
aws sts get-caller-identity --query Account --output text

# Get current region
aws configure get region

# Get current access key (ID only, not the secret)
aws configure get aws_access_key_id
```

## IAM Permissions Required

Your AWS user/role needs these permissions:
- `ecr:*` (for ECR operations)
- `sts:GetCallerIdentity` (for account verification)

## Test Setup

After adding secrets, trigger the workflow:
```bash
git commit --allow-empty -m "trigger workflow"
git push origin gitops
```
