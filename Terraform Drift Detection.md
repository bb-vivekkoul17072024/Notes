# Terraform Drift Detection Using Jenkins Pipeline

## Overview
This document describes how to set up a Jenkins pipeline to detect Terraform drift using a scripted pipeline approach. The pipeline will fetch Terraform code from a Git repository, execute Terraform commands, and check for infrastructure drift.

---

## Step 1: Store Terraform Code in a Git Repository
If your Terraform code is on your local VS Code, push it to a Git repository (e.g., GitHub, GitLab, or Bitbucket).

### Steps to Push Terraform Code to GitHub:
```sh
cd /path/to/your/terraform/code
git init
git add .
git commit -m "Initial Terraform code"
git branch -M main
git remote add origin <your-git-repo-url>
git push -u origin main
```
Jenkins will fetch this repository during pipeline execution.

---

## Step 2: Configure Jenkins to Use a Scripted Pipeline
Since we are writing the pipeline script directly, follow these steps:
1. Go to **Jenkins Dashboard** → **New Item** → Select **Pipeline** → Enter Job Name.
2. Check **This project is parameterized** and add the parameter (explained in Step 3).
3. In **Pipeline Definition**, select **Pipeline script** and enter the script below.
4. Click **Save**.

---

## Step 3: Add a Parameter for Checking Plan
1. In Jenkins Pipeline Job, go to **This project is parameterized**.
2. Click **Add Parameter** → Select **Boolean Parameter**.
3. Enter:
   - **Name:** `CHECK_PLAN_ONLY`
   - **Default Value:** `true`
   - **Description:** Check for drift without applying changes.

---

## Step 4: Ensure Terraform is Installed on Jenkins
Jenkins needs Terraform to execute commands. If it's not installed, install it using the following commands:
```sh
sudo apt-get update && sudo apt-get install -y terraform
terraform -version  # Verify installation
```
Ensure the Jenkins user has the necessary permissions:
```sh
sudo chmod +x /usr/local/bin/terraform
```

---

## Step 5: Jenkins Pipeline Script
Below is the pipeline script used for Terraform drift detection:

```groovy
pipeline {
    agent any
    environment {
        AWS_REGION = 'ap-south-1'
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    git branch: 'master', url: 'https://github.com/bb-vivekkoul17072024/Terraform-codes.git'
                }
            }
        }
        stage('Terraform Init') {
            steps {
                script {
                    dir('ec2-instance') {
                        sh 'terraform init'
                    }
                }
            }
        }
        stage('Terraform Plan') {
            steps {
                script {
                    dir('ec2-instance') {
                        sh 'terraform plan -out=tfplan'
                    }
                }
            }
        }
    }
}


```

---

## Step 6: Run the Pipeline
1. Click **Build Now** in Jenkins.
2. The pipeline will:
   - Clone Terraform code from GitHub.
   - Run `terraform init`.
   - Run `terraform plan` to check for drift.
   - If `CHECK_PLAN_ONLY=false`, it will apply changes to fix drift.

---

## Conclusion
This Jenkins pipeline allows automated detection of infrastructure drift using Terraform. The parameter `CHECK_PLAN_ONLY` lets users decide whether to apply changes or just check for drift.

Use this setup to maintain infrastructure consistency and detect changes before they cause issues.

