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
## Misconfigured Lambda Alias Routing

Lambda includes a mechanism for distributing traffic by generating one or more function aliases. An alias represents the use of numerous versions of a Lambda function. We can now divide the traffic for the various lambda function using alias routing.

Depending on this, an application may occasionally load different lambda function instances. If the application has any security flaws such as SSRF, LFI, etc when obtaining the resource from a user-provided URL parameter. 

Using the above vulnerability, the attacker can retrieve internal files and access the lambda environment variables which lead to sensitive information disclosures, access to the S3 bucket, or privilege escalation in AWS. 

#### How To Test the Vulnerability :
```
1. Navigate to a domain that hosts a Cloud-based App.
2. Now try to search for parameters like 'url', 'file' which could you used to pull resources from the application.
3. Create a bash script to run a loop for about 50 req on the application
4. Also add the following payload: file:///proc/self/environ to check if any instances of the lambda function provide a different response containing the environment variables for the lambda function
5. Finally, if the application is vulnerable we could now dump env variables
```
## Denial of Wallet (DOW)

Denial of Wallet is a denial of service (DOS) based vulnerability in which the attacker could upload a very large file which might incur costs within the AWS which might lead to bankruptcy of companies due to high amount of charges.

Denial-of-Service attacks take advantage of the fact that serverless suppliers charge customers based on the amount of resources needed by an application, which means that if an attacker floods a website with traffic, the site owner could be hit with a hefty bill.

DoW attacks involve the deliberate, repeated invocation of serverless functions, leaving the victim with inflated consumption bills and a depleted financial state. Excessive function run time, a high number of invocations, and higher resource use all raise execution costs.

#### How To Test the Vulnerability :
```
1. Register within the Application
2. Now search for a file upload features to upload documents
3. Try to test whether we can upload a large amount of files within the application.
4. If we can upload very large files (GBs), then app is vulnerable.
```
##### References: [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S221421262100079X)       [Portswigger](https://portswigger.net/daily-swig/denial-of-wallet-attacks-how-to-protect-against-costly-exploits-targeting-serverless-setups)        [Medium](https://medium.com/geekculture/denial-of-wallet-attack-3d8ecadfbd4e)

## Exfiltrating Lambda Event Data

An attacker can query the lambda runtime API endpoint and steal event data if they were able to run commands on the system. This data is made available to the function via the runtime interface.

Lambda functions also have event data that is passed to the function when it is started. Unlike IAM credentials, this data is accessible over standard SSRF at:
```
http://localhost:9001/2018-06-01/runtime/invocation/next
```
#### Important Environment Variables:
``` 
-> _HANDLER: Location to the handler.
–> LAMBDA_TASK_ROOT – The directory that contains the function code.
-> AWS_LAMBDA_RUNTIME_API – The host and port of the runtime API: 127.0.0.1:9001.
```
#### Lambda Runtime API Methods:
```
-> Next Invocation: GET /runtime/invocation/next
-> Invocation response : POST /runtime/invocation/AwsRequestId/response
-> Invocation error: POST /runtime/invocation/AwsRequestId/error
-> Initialization error Path: POST /runtime/init/error
```
#### References: [AWS](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-api.html)        [Hackingthe](https://hackingthe.cloud/aws/exploitation/lambda-steal-iam-credentials/)

## Lambda Backdoor

Lambda Backdoor is a mechanism for an attacker to maintain access to AWS by creating a cross-account role and attaching a lambda function to that role. Now an attacker can utilize this lambda function to exfiltrate data to its own server and get administrator access to AWS.

#### Steps To Create Lambda Backdoor:
```
1. Create Cross Account Privilege Role.
2. Create a Lambda Service Role.
3. Now customize the function runtime and set up a listener to accept the data from the lambda function.
```
#### References: [Hackingthe](https://hackingthe.cloud/aws/post_exploitation/lambda_persistence/)        [Frichetten](https://frichetten.com/blog/revisiting_lambda_persistence/)        [Paloaltonetworks](https://unit42.paloaltonetworks.com/gaining-persistency-vulnerable-lambdas/)

https://labs.detectify.com/2022/07/25/aws-services-security-vulnerabilities-exploitation-remediation/


# [More info](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
