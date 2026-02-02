# Intelligent Content Moderation

This project demonstrates an event-driven AWS-based content moderation pipeline. Files uploaded to Amazon S3 automatically trigger a processing workflow that runs inside an ECS task and analyzes the content.

The goal of this project is to provide a technical foundation for automated content or threat analysis, with the option to later integrate real AI/ML models.

🏗️ Architecture Overview

+ A file is uploaded to an S3 bucket
+ The upload event triggers an AWS Lambda function
+ The Lambda function starts an ECS task
+ The ECS task runs a container built from the provided Dockerfile
+ The application inside the container (app.py) analyzes the file and returns a result
+ This setup enables scalable, event-driven processing of uploaded content.

🚀 Deployment Steps

1️⃣ Configure AWS Credentials

Make sure your AWS CLI is configured:
```
aws configure
```
2️⃣ Deploy Infrastructure with Terraform

Navigate to the Terraform directory and run:
```
terraform init
terraform plan
terraform apply
```

This will create resources such as:

+ S3 bucket
+ Lambda function
+ IAM roles and policies
+ ECS cluster and task definition

3️⃣ Configure IAM Permissions

Update the file:
````
IAM/policy.json
````

Adjust permissions according to your AWS environment and security requirements, then attach the policy to the appropriate roles.

4️⃣ Configure Lambda Environment Variables

Edit the Lambda configuration to match your setup.
The file:
````
Lambda/handler.py
````
expects environment variables (such as ECS cluster name, task definition, subnet IDs, etc.). These must be set in the Lambda environment in AWS.

5️⃣ Build and Push the Docker Image

Build the Docker image:
````
docker build -t intelligent-moderation .
````
Tag and push it to Amazon ECR:
````
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <account-id>.dkr.ecr.<region>.amazonaws.com
docker tag intelligent-moderation:latest <account-id>.dkr.ecr.<region>.amazonaws.com/intelligent-moderation:latest
docker push <account-id>.dkr.ecr.<region>.amazonaws.com/intelligent-moderation:latest
````

Make sure your ECS task definition uses this image.

🧠 How It Works

+ Upload a file to the configured S3 bucket
+ The Lambda function is triggered by the S3 event
+ Lambda starts a new ECS task
+ The container runs app.py
+ The file is analyzed and a response is generated

🔮 Future Improvements

This project currently provides the infrastructure and workflow for automated analysis. The next step is to integrate a real AI model for intelligent threat or content detection, such as:

+ Image moderation
+ Text classification
+ Malware detection
+ Threat intelligence analysis
+ Possible integrations:
+ Amazon Rekognition
+ Amazon Comprehend
+ Custom ML models via SageMaker
+ External AI APIs
