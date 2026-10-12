# AWS S3 Static Website Deployment using GitHub Actions

A beginner-friendly Cloud/DevOps project that demonstrates how to deploy
a static website to **Amazon S3** automatically using **GitHub
Actions**.

## Project Overview

This project uses GitHub Actions to upload website files from a GitHub
repository to an Amazon S3 bucket whenever code is pushed to the `main`
branch.

### Tools and Services

-   **Amazon S3** --- stores and hosts the static website files
-   **AWS IAM** --- controls deployment permissions
-   **GitHub** --- source code repository
-   **GitHub Actions** --- automates the deployment (CI/CD)
-   **AWS CLI** --- syncs the website files to S3

## Architecture

``` text
Developer
   |
   | git push
   v
GitHub Repository (main)
   |
   v
GitHub Actions Workflow
   |
   | AWS credentials from GitHub Secrets
   v
Amazon S3 Bucket
   |
   v
Static Website Endpoint
```

## Repository Structure

``` text
aws-s3-static-website-cicd/
├── .github/
│   └── workflows/
│       └── main.yml
├── index.html
├── style.css
├── script.js
└── README.md
```

> Your workflow filename may be different. Update the structure above to
> match your repository.

## AWS Setup

1.  Create an S3 bucket in your preferred AWS Region.
2.  Enable **Static website hosting** in the bucket's **Properties**
    tab.
3.  Set the index document to `index.html`.
4.  Note the bucket name, Region, and website endpoint.
5.  Create a dedicated IAM identity with only the permissions required
    to deploy to this bucket.

For a direct S3 website endpoint, configure access appropriately. S3
website endpoints do not support HTTPS. For a more secure production
setup, keep the bucket private and use Amazon CloudFront with Origin
Access Control.

## GitHub Secrets and Variables

In your GitHub repository, open:

**Settings → Secrets and variables → Actions**

Add these repository secrets if your workflow uses IAM access keys:

  -----------------------------------------------------------------------
  Name                                Value
  ----------------------------------- -----------------------------------
  `AWS_ACCESS_KEY_ID`                 Access key ID for the dedicated
                                      deployment IAM user

  `AWS_SECRET_ACCESS_KEY`             Secret access key for that IAM user
  -----------------------------------------------------------------------

Add this repository variable:

  Name               Value
  ------------------ ---------------------------
  `S3_BUCKET_NAME`   Your exact S3 bucket name

Use the AWS Region where your bucket was created. This project currently
uses **Mumbai (`ap-south-1`)**.

**Security:** Never commit AWS credentials to the repository or share
them publicly. Do not use an IAM user's administrator credentials.
Prefer GitHub Actions OIDC with short-lived credentials when you are
ready to configure it.

## GitHub Actions Workflow

The workflow should:

1.  Check out the repository.
2.  Configure AWS credentials.
3.  Sync the website files to the S3 bucket.

Example deployment command:

``` bash
aws s3 sync . s3://YOUR-BUCKET-NAME \
  --delete \
  --exclude ".git/*" \
  --exclude ".github/*" \
  --exclude "README.md"
```

Replace `YOUR-BUCKET-NAME` with your bucket name. The `--delete` option
removes objects from the destination bucket that are not present in the
source directory. Use it only when that behavior is intended.

## How to Deploy

1.  Add or update your website files in the repository.
2.  Commit and push the changes to the `main` branch.
3.  Open the **Actions** tab in GitHub.
4.  Select the deployment workflow and inspect the run.
5.  Confirm that all workflow steps succeed.
6.  Open the S3 static website endpoint to check the website.

Every new push to `main` can trigger another deployment, depending on
your workflow configuration.

## Troubleshooting

  -----------------------------------------------------------------------
  Error                               What to check
  ----------------------------------- -----------------------------------
  `Unable to locate credentials`      Check that the GitHub secret names
                                      match the workflow.

  `AccessDenied`                      Check the IAM permissions and
                                      bucket policy.

  `NoSuchBucket`                      Verify the bucket name and Region.

  `Invalid workflow file`             Check YAML syntax and indentation.

  Website shows `403 Forbidden`       Check the S3 website access
                                      configuration and permissions.

  Website shows `404 Not Found`       Confirm that `index.html` was
                                      uploaded and configured as the
                                      index document.
  -----------------------------------------------------------------------

## What I Learned

-   Creating and configuring an S3 static website
-   Using IAM permissions for a deployment task
-   Managing GitHub Actions secrets
-   Automating deployments with a CI/CD workflow
-   Troubleshooting AWS deployment errors

## Project Status

**In progress** --- configuring and testing the GitHub Actions
deployment workflow.

## Author

**Roshani Shinde**

Cloud & DevOps Learner \| AWS \| Linux \| Docker \| GitHub Actions
