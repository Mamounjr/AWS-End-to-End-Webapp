# AWS-End-to-End-Webapp
Developing a functional web application on AWS by integrating Amplify, Lambda, IAM, API Gateway, and DynamoDB.

This portfolio project focuses on implementing an AWS web application with an emphasis on security, resilience, and reproducibility.

#Architecture
Frontend: Amplify
Serverless: Lambda 
API Gateway: Restful API
Database: DynamoDB

STEP 1: Deployed app in Amplify
STEP 2: Deployed Lambda function
STEP 3: Implemented API gateway to trigger the Lambda Function
STEP 4: Incorporate Database using DynamoDB to store and retrieve results


## Security Enhancements: IAM Least Privilege

To enforce the principle of **least privilege**, the Lambda execution role was restricted to only the DynamoDB actions required by the application.

- **Inline policy:** Limited to `dynamodb:PutItem` on the specific DynamoDB table ARN (account ID redacted for security).
- **Benefit:** Reduces risk of accidental data exposure or modification, while still allowing the Lambda function to insert new math results.

This demonstrates secure role design and adherence to cloud security best practices.





