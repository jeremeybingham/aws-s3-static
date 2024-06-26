# 💽 S3 Static Resume with GitHub Actions CI/CD

This repository contains the code for: [aws-s3-static.jeremeybingham.com](https://aws-s3-static.jeremeybingham.com).

### Some other resume templates in progress, inspired by the [Cloud Resume Challenge](https://cloudresumechallenge.dev/docs/the-challenge/aws/):

🌤️ **Google Cloud Run/Docker/CI/CD** version: [gcp-resume.jeremeybingham.com](https://gcp-resume.jeremeybingham.com) 
repo/code: [gcp-resume](https://github.com/jeremeybingham/gcp-resume)

📝 **S3 Static via Terraform** version: [resume.jeremeybingham.com](https://resume.jeremeybingham.com) 
repo/code: [gcp-resume](https://github.com/jeremeybingham/resume)

## 🚀 Deployment & Features

- 🔍 Monitors `main` branch for changes.
- 🪣 Updates S3 bucket content.
- 🔒 Uses GitHub Secrets for IAM-based token.

Be sure to add your IAM token to GitHub secrets:
   - `AWS_ACCESS_KEY_ID`
   - `AWS_SECRET_ACCESS_KEY`

Set up GitHub Actions workflow as follows:
   ```yaml
   name: Deploy to S3
   
   on:
     push:
       branches:
         - main
   
   jobs:
     deploy:
       runs-on: ubuntu-latest
       
       steps:
       - name: Checkout code
         uses: actions/checkout@v2
       
       - name: Sync to S3
         run: |
           aws s3 sync . s3://your-bucket-name --delete
         env:
           AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
           AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
