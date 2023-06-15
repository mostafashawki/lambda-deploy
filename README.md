# Deploying a Lambda Function using GitHub Actions

This repository demonstrates how to deploy a Lambda function using GitHub Actions and the AWS Command Line Interface (CLI). The deployment process is triggered automatically whenever changes are pushed to the `main` branch.

## Prerequisites

Before getting started, make sure you have the following prerequisites:

1. An AWS account: You'll need an AWS account to create and deploy the Lambda function.

2. GitHub repository: Create a GitHub repository to host your code and workflow.

3. AWS CLI: Install and configure the AWS CLI on your local development environment. You can refer to the [AWS CLI documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html) for installation instructions.

## Repository Structure

The repository has the following structure:

```
.
├── .github
│   └── workflows
│       └── deploy-lambda.yml
├── index.js
├── package.json
└── README.md
```

- `index.js`: Contains the sample code for the Lambda function.

- `package.json`: Includes the project metadata and dependencies.

- `.github/workflows/deploy-lambda.yml`: Defines the GitHub Actions workflow for deploying the Lambda function.

## Usage

Follow these steps to deploy the Lambda function using GitHub Actions:

1. Fork this repository: Click the "Fork" button at the top-right corner of this repository to create a fork in your GitHub account.

2. AWS IAM Role: Create an IAM role in the AWS Management Console that grants the necessary permissions to the Lambda function. To create the role, you can use the following AWS CLI command:

   ```bash
   aws iam create-role \
     --role-name lambda-role \
     --assume-role-policy-document '{
       "Version": "2012-10-17",
       "Statement": [
         {
           "Sid": "",
           "Effect": "Allow",
           "Principal": {
             "Service": "lambda.amazonaws.com"
           },
           "Action": "sts:AssumeRole"
         }
       ]
     }'
   ```

   Retrieve the ARN (Amazon Resource Name) of the created IAM role, as it will be needed in the next step.

3. GitHub repository secrets: In your GitHub repository settings, add the following secrets:

   - `AWS_ACCESS_KEY_ID`: Your AWS access key ID.
   - `AWS_SECRET_ACCESS_KEY`: Your AWS secret access key.
   - `AWS_DEFAULT_REGION`: The AWS region where you want to deploy the Lambda function.

4. Update the workflow file: Open the `.github/workflows/deploy-lambda.yml` file in your repository, and make the following changes:

   - Replace `YOUR_LAMBDA_FUNCTION_NAME` with the name you want to give to your Lambda function.
   - Replace `YOUR_AWS_ROLE_ARN` with the ARN of the IAM role you created in step 2.

5. Commit and push changes: Save the changes to the workflow file and commit them to the `main` branch of your repository.

6. Deployment: Once the changes are pushed, the GitHub Actions workflow will automatically trigger, deploying the Lambda function using the AWS CLI.

   **Note**: For the initial deployment, you need to manually create the Lambda function in the AWS Management Console with the same name and region as specified in the workflow file. This allows the workflow to update the function in subsequent deployments.

That's it! The Lambda function will be deployed automatically whenever changes are pushed to the `main` branch of your repository. You can view the workflow execution details in the "Actions" tab of your GitHub repository.

---

Please make sure to replace

 `YOUR_LAMBDA_FUNCTION_NAME` with the desired name for your Lambda function, and `YOUR_AWS_ROLE_ARN` with the actual ARN of the IAM role you created in step 2.
