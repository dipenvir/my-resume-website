# Resume Website CI/CD Pipeline Documentation

## 1. Pipeline Overview

This project automates the deployment of a static HTML/CSS resume website to AWS S3 using a CI/CD pipeline.  
The pipeline monitors a **GitHub repository** for changes and automatically deploys updates to the website.

**Pipeline Architecture:**
+-----------------+      +-----------------+      +----------------+
|                 |      |                 |      |                |
|   GitHub Repo   +----->+   CodeBuild     +----->+   S3 Bucket    |
|                 |      | (Build Stage)   |      | (Deploy Site)  |
+-----------------+      +-----------------+      +----------------+

**Stage Description:**

1. **Source Stage (GitHub)**
   - Monitors the `main` branch of the GitHub repository.
   - Triggers the pipeline automatically via **webhooks** on every commit.

2. **Build Stage (AWS CodeBuild)**
   - Runs a build project to package website files.
   - Uses `buildspec.yml` to define build commands and artifacts.
   - For static HTML/CSS, the build stage simply passes files to the deploy stage.

3. **Deploy Stage (Amazon S3)**
   - Deploys packaged files to an S3 bucket configured for static website hosting.
   - The S3 bucket has **public access enabled** for website availability.

---

## 2. Setup Instructions

### Step 1: GitHub Repository
1. Create a GitHub repository (e.g., `my-resume-website`).
2. Push your website code:

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/<username>/my-resume-website.git
git push -u origin main
```
## 5. Troubleshooting
1. 403 Forbidden on website: Ensure S3 bucket policy allows public read, static website hosting is     enabled, and use the website endpoint URL.

2. Pipeline fails to trigger: Check GitHub webhooks and CodePipeline permissions.

3. CodeBuild fails: Check buildspec.yml syntax and ensure CodeBuild service role has access to S3.

4. Website not updating: Verify artifacts are correctly output in CodeBuild, and deploy stage points to the correct S3 bucket.

