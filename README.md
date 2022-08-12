# AWSSecurity

## Introduction To AWS

Amazon's AWS is the world's most popular cloud computing plateform. It offers a variety of services such as storage, computing, networking, security, scalability and reliability providing a pay-as-go business model.

#### Shared Responsibility Model

AWS employs a security and compliance paradigm known as the shared resposibility model. The shared responsibility makes sure that AWS manages "Security of the Cloud" by controlling the hardware, software, networking and underlying data center.

The AWS Customer is in charge of assuring "Security in the Cloud" which means that all resources that the customer deploys must have their security taken care of separately. From managing the OS, software updates, security groups etc. should be handled by AWS Customer.

#### Common Services in AWS

```
1. Elastic Compute Cloud (EC2) : Launching & Managing your Instances.
2. Elastic Block Storage (EBS) & Elastic File System (EFS) : Store Data on Instances.
3. Identity Access Management (IAM) : Manages access to services/resources via IAM Policies.
4. Lambda (Serverless) : Function-as-Service
5. Relational Database (RDS, MariaDB, Oracle, Postgres, Aurora) : Used for storing data using RDBMS.
6. NoSQL Database (DynamoDB, DocumentDB, Neptune, Redis, DAX, ElasticSearch) : Used for stored data using non-relational database.
7. VPC (Networking)
8. Route53 (DNS)
9. AWS cognito & SSO (Delegated Access to resources using federation)
10. Cloudwatch  (Monitoring & Alerting Service)
11. Cloudtrail (Logging Malicious API Calls)
12. Config (Resources Compliance and Configuration Management)
13. Simple Queue Service (SQS) & Simple Notification Service (SNS) : Messaging Services
14. S3 & Amazon Fsx (Storage Services)
15. AWS Data Sync & Snow Family (Data Migration)
16. AWS Backups & Elastic Disaster Recovery (Disaster Recovery)
17. Security Groups & NACL (Firewalls)
18. Elastic Container Service (ECS) & Fargate (Container Services)
19. Elatic Kubernetes Service (EKS) 
20. AWS WAF, Shield, Inspertor, Guarduty (Security Services)
21. Key Management Service (KMS)
22. Cloud Foramtion (Resource Management & Deployment)
```
#### Advantages of AWS
```
-> Security
-> Scalability
-> Reliability
-> Cost-Effective
-> Easy to Use
-> Fflexibility
```

## Introduction To Lambda (Serverless)

Lambda is a computing service that enables us to run programs without having to manage servers. As a result of their event-driven nature and ability to run code on a managed pool of computing resources, they are also known as function-as-services (FAAS).

#### Lambda Definitions:

```
Function: A function is a resource that you can use to run your code in Lambda.

Trigger: A trigger is a resource or configuration that calls a Lambda function.

Event: An event is a JSON-formatted document that includes data for a Lambda function to process. 

Execution Environment: An execution environment gives your Lambda function a safe and isolated runtime environment. 

Deployment Package:  You use a deployment package to distribute the Lambda function code. The two deployment packages are zip & container images.

Runtime: The runtime offers a language-specific environment that operates in an execution environment.

Layer:  A Lambda layer is a zip file archive that can include additional code containing libraries, a custom runtime, data, or configuration files. There can be up to 5 layers.

Destination: The place where Lambda can transmit events from an asynchronous invocation is known as a destination.
```
#### The Cost for the lambda function depends on 2 factors:

Compute Time: The cost depends on the total duration of time the function has been run and also the amount of memory being provisioned, measured in GB seconds. 
No of Requests: The charges are incurred for every million requests per month.

#### Lambda Features:

```
-> Concurrency & Scaling Controls
-> Functions defined as Container Images
-> Code Signing
-> Lambda Extensions
-> Function Blueprints
-> File System Access
-> Database Access
```
#### Important Lambda Commands:
1. Returns information about a version of an AWS Lambda layer
```
aws lambda get-layer-version --layer-name <value> --version-number <value>
```
2. Lists event source mappings.
```
aws lambda list-event-source-mappings
```
3. Returns the permission policy for a version of an AWS Lambda layer.
```
aws lambda get-layer-version-policy --layer-name <value> --version-number <value>
```
4. Invokes a Lambda function.
```
aws lambda invoke --function-name <value>
```
5. Retrieves details about your account's limits and usage in an AWS Region.
```
aws lambda get-account-settings
```
6. Returns a list of code signing configurations.
```
aws lambda list-code-signing-configs
```
7. Returns information about specified code signing configuration
```
aws lambda get-code-signing-config --code-signing-config-arn <value>
```
8. Returns a list of versions, with the version-specific configuration of each
```
aws lambda list-versions-by-function --function-name value
```  
9. Creates an AWS Lambda layer from a ZIP archive.
```
aws lambda publish-layer-version --layer-name <value>
```
10. Creates a version from the current code and configuration of a function.
```
aws lambda publish-version --function-name <value>
```  
11. Updates the configuration of a Lambda function alias.
```
aws lambda update-alias --function-name <value>
```
12. Deletes a Lambda function alias.
```
aws lambda delete-alias --function-name <value> --name <value>
```  
13. Deletes a Lambda function.
```
aws lambda delete-function --function-name <value>
```
14. Deletes a version of an AWS Lambda layer.
```
aws lambda delete-layer-version --layer-name <value> --version-number <value>
```
# [More info](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
