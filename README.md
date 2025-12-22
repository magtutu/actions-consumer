# Actions Consumer

This repository demonstrates how to consume reusable workflows from another repository.

## About

This repo calls the `on-merge.yml` workflow from the shared-actions repository. All environments, secrets, and protection rules are managed centrally in the shared-actions repo.

## Setup Instructions

1. **Update workflow file**: In `.github/workflows/merge-main.yml`, replace `magtutu` with your GitHub username

2. **Ensure naming convention**: The `app-name` should match your repository name (`actions-consumer`)

3. **That's it!** No environments or secrets needed in this repo. Everything is managed in the shared-actions repository.

## How It Works

- This repo calls `on-merge.yml` from shared-actions on every push to main
- The workflow runs in the shared-actions repo context
- Secrets come from shared-actions repo environments
- Protection rules (approvals, branch restrictions) are enforced from shared-actions
- The pipeline automatically: deploys to staging → waits for approval → deploys to production

## Deployment Flow

```
Push to main
    ↓
on-merge.yml (in shared-actions)
    ↓
Deploy to Staging (automatic)
    ↓
Wait for Approval (if configured)
    ↓
Deploy to Production
```

## Testing

**Trigger deployment**:
```bash
git add .
git commit -m "Test deployment"
git push origin main
```

This will:
1. Automatically deploy to staging
2. Pause for approval (if you configured reviewers in shared-actions production environment)
3. Deploy to production after approval

## What You'll Learn

- How to call reusable workflows from another repository
- How centralized environments work with reusable workflows
- How protection rules apply across repositories
- How to pass inputs to reusable workflows
- How workflow access control works
- How approval gates work in deployment pipelines
