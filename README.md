# AWS-End-to-End-Webapp

Developing a functional web application on AWS by integrating **Amplify, API Gateway, Lambda, IAM, and DynamoDB**.  
This project demonstrates how to build and secure a **three-tier serverless web application** with emphasis on **security, resilience, and reproducibility**.

---

## Project Overview
This portfolio project showcases how AWS services can be combined to deliver a secure, serverless web application.  
It highlights:
- End-to-end architecture (frontend → backend → database)
- Security best practices (IAM least privilege, CloudTrail, WAF, encryption)
- Professional documentation and reproducibility

---

## Architecture Diagram

**Secure Three-Tier Serverless Architecture (AWS)**

- **Presentation tier:** Amazon Amplify hosts the frontend.  
- **Application tier:** API Gateway routes requests to AWS Lambda, which executes business logic.  
- **Data tier:** Amazon DynamoDB stores and retrieves results.  
- **Security layer:** IAM, WAF, CloudTrail, KMS, and SNS provide defense-in-depth.  

---

## AWS Services Used

- **Amazon Amplify** → Frontend hosting and deployment  
- **Amazon API Gateway** → RESTful API routing  
- **AWS Lambda** → Serverless compute for backend logic  
- **Amazon DynamoDB** → NoSQL database for storing results  
- **AWS IAM** → Role-based access control with least privilege  
- **AWS WAF** → Web Application Firewall protecting API Gateway  
- **AWS CloudTrail** → Auditing and logging of API activity  
- **Amazon S3 (with KMS)** → Encrypted storage of CloudTrail logs  
- **Amazon SNS** → Notifications when new logs are delivered  
- *(Optional, not enabled)* **Amazon CloudWatch** → Would be used for monitoring and alarms in production  

---

## Implementation Steps

1. **Frontend:** Deployed app in Amplify  
2. **Backend:** Created Lambda function for business logic  
3. **API Gateway:** Configured RESTful API to trigger Lambda  
4. **Database:** Integrated DynamoDB to store and retrieve results  
5. **Security Enhancements:** Applied IAM least privilege, CloudTrail auditing, WAF, and encryption  

---

## Security Enhancements

### IAM Least Privilege
- Lambda execution role restricted to only the DynamoDB actions required (`dynamodb:PutItem`).  
- Scoped to the specific DynamoDB table ARN (account ID redacted).  
- **Benefit:** Prevents accidental data exposure or modification.

### CloudTrail Auditing
- Configured trail to capture all management events across all Regions.  
- Logs delivered to S3 with **KMS encryption** enabled.  
- **SNS topic** sends notifications when new logs are delivered.  
- **Benefit:** Provides a tamper-resistant audit trail of API activity.

### AWS WAF
- WAF enabled and associated with API Gateway stage.  
- Documented rule categories: SQL injection, XSS, rate limiting.  
- **Benefit:** Protects against common web exploits.

### API Gateway CORS Restriction
- Configured to allow requests only from Amplify domain.  
- **Benefit:** Prevents unauthorized cross-origin requests.

### Encryption at Rest 
- DynamoDB encrypted with AWS-managed KMS keys (default). 
- CloudTrail logs encrypted with a **customer-managed KMS key** in S3.
-  **Benefit:** Ensures sensitive data and audit logs are protected at rest.

---

## Threat Model

This project applies a basic threat modeling approach to identify key assets, potential threats, and the controls used to mitigate them.

## Assets
- **Application frontend:** Deployed via Amazon Amplify
- **Backend logic:** AWS Lambda function behind API Gateway.
- **Data:** Math operation results stored in DynamoDB.
- **Audit data:** CloudTrail logs stored in an encrypted S3 bucket.

## Key Threats
- **Unauthorized access to data:** Attackers attempting to read or modify stored results.
- **Abuse of API endpoints: **High or malicious requests targeting the API (e.g., brute force, basic DoS).
- **Misuse of AWS credentials or permissions:**Overly permissive IAM roles or compromised access keys
- **CORS restrictions:** API Gateway is configured to accept requests only from the Amplify frontend domain, reducing unauthorized cross-origin access.
- **Encryption at rest:** DynamoDB and CloudTrail logs are protected using AWS KMS, limiting exposure if storage is accessed.

### Residual Risks and Future Enhancements 
- **Monitoring and alerting:** CloudWatch metrics and alarms were not enabled in this build to avoid costs, but would be used in production to detect anomalies (e.g., spikes in 4xx/5xx errors, Lambda throttling).
- **Secrets management:** For larger or more complex applications, AWS Systems Manager Parameter Store or AWS Secrets Manager would be used to store configuration and secrets instead of hardcoding values. This threat model demonstrates a structured approach to thinking about risks and applying practical security controls in a serverless architecture.

---

## Lessons Learned
- How to classify serverless apps as **three-tier architectures**.  
- The importance of **least privilege IAM policies** in real-world deployments.  
- How **CloudTrail** provides governance and auditability for API activity.   

---

## Skills Demonstrated
- AWS services: Amplify, API Gateway, Lambda, DynamoDB, IAM, CloudTrail, WAF, S3, SNS  
- Security principles: Least privilege, encryption, monitoring, auditing  
