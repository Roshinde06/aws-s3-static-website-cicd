# AWS Static Website Hosting with CI/CD using GitHub Actions

## 📌 Project Overview

This project demonstrates static website hosting using Amazon S3, with GitHub Actions for automated deployment and Amazon CloudFront for content delivery.

I configured AWS resources using the **AWS Management Console (GUI)** and created a GitHub Actions workflow to automate website deployment.

**Project status:** Completed as a hands-on learning exercise. AWS resources were removed after testing to avoid unnecessary costs. The previous CloudFront URL may no longer be active.

## 🛠️ Technologies Used

- **Amazon S3** – Static website hosting and file storage
- **Amazon CloudFront** – Content delivery and caching
- **GitHub Actions** – CI/CD workflow automation
- **AWS IAM** – Access and permission management
- **AWS Management Console** – AWS resource configuration
- **GitHub Secrets and Variables** – Deployment credentials and configuration

## 🏗️ Architecture

Developer → GitHub Repository → GitHub Actions → Amazon S3 → Static Website

Amazon CloudFront was configured for content delivery and caching.

## ✨ Project Features

- Hosted a static portfolio website using Amazon S3.
- Configured CloudFront for content delivery.
- Created a GitHub Actions workflow triggered by pushes to the `main` branch.
- Automated website file synchronization to S3.
- Configured GitHub repository secrets and variables.
- Added a CloudFront cache invalidation step to the deployment workflow.
- Practised troubleshooting AWS credentials, configuration, and permissions.

## 📂 Repository Structure

```text
aws-s3-static-website-cicd/
├── .github/
│   └── workflows/
│       └── main.yml
├── cloud_devops_portfolio/
│   ├── index.html
│   ├── style.css
│   └── script.js
└── README.md
```

*Adjust the filenames if your actual repository structure differs.*

## ⚙️ CI/CD Workflow

1. Push website changes to the `main` branch.
2. GitHub Actions checks out the repository.
3. AWS credentials are configured using GitHub Secrets.
4. Website files are synchronized with the S3 bucket.
5. The workflow requests CloudFront cache invalidation to help deliver updated content.

The CloudFront invalidation step requires a valid distribution ID and appropriate IAM permissions.

## 🔐 GitHub Configuration

### Repository Secrets

| Secret | Purpose |
|---|---|
| `AWS_ACCESS_KEY_ID` | AWS access key |
| `AWS_SECRET_ACCESS_KEY` | AWS secret access key |

### Repository Variables

| Variable | Purpose |
|---|---|
| `S3_BUCKET_NAME` | Target S3 bucket name |
| `CLOUDFRONT_DISTRIBUTION_ID` | CloudFront distribution ID |

**Security:** Never commit AWS credentials or tokens to GitHub. Use GitHub Secrets and appropriately scoped IAM permissions.

## 📚 What I Learned

- Static website hosting with Amazon S3.
- Configuring AWS services through the management console.
- Automating deployments using GitHub Actions.
- Managing repository secrets and variables.
- Understanding AWS IAM permissions and CloudFront cache invalidation.
- Troubleshooting CI/CD workflow errors.
- Managing cloud costs by removing unused resources.

## 🚧 Challenges and Improvements

During this project, I practised troubleshooting deployment configuration and AWS permissions. I also learned the importance of verifying each pipeline step and monitoring cloud costs.

Possible future improvements:
- Use GitHub Actions OIDC with an IAM role instead of long-lived access keys.
- Add automated website validation.
- Improve pipeline error handling.
- Recreate the infrastructure when needed while monitoring costs.

## 🔗 GitHub Repository

https://github.com/Roshinde06/aws-s3-static-website-cicd

---

*This project is part of my practical learning journey in AWS, Cloud Computing, and DevOps.*
