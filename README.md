# Data Transfer Hub

_Note_: If you have already deployed this solution, refer to the [User Guide](../../../Downloads/data-transfer-hub-main/docs/UserManual.md).

Data Transfer Hub is a secure, reliable, scalable, and trackable solution offers a unified user experience that 
allows you to easily create and manage different types of data transfer tasks from different sources to 
Amazon Web Services cloud-native services. You can launch this solution and start to replicate data within a few minutes.

With Data Transfer Hub, you can perform any of the following tasks:
- Transfer Amazon S3 objects between AWS China Regions and AWS Regions.
- Transfer Amazon S3 objects between AWS GovCloud and AWS Regions.
- Transfer data from other cloud providers’ object storage services (including Alibaba
Cloud OSS, Tencent COS, Qiniu Kodo, and S3 Compatible storage) to Amazon S3.
- Transfer Amazon ECR images between AWS China Regions and AWS Regions.
- Transfer container images from public container registries (e.g., Docker Hub, Google
gcr.io, Red Hat Quay.io) to Amazon ECR.

![](../../../Downloads/data-transfer-hub-main/docs/images/homepage.png)

## Features

- [x] Authentication (Cognito User Pool, OIDC)
- [x] Self-service User Interface
- [x] CDK Deployment
- [x] CloudFormation Deployment
- [x] S3 Plugin
    - [x] Amazon S3 object copy between AWS China Regions and AWS Regions.
    - [x] Amazon S3 object copy between AWS GovCloud and AWS Regions.
    - [x] Data transfer from Alibaba Cloud OSS to Amazon S3
    - [x] Data transfer from Tencent COS to Amazon S3
    - [x] Data transfer from Qiniu Kodo to Amazon S3
    - [x] Support data transfer with Metadata
    - [x] Support S3 Events to trigger data transfer
    - [x] Use TCP BBR to improve network performance.
    - [x] Support transfer from Amazon S3 Compatible Storage
- [x] ECR Plugin
    - [x] Amazon ECR images copy between AWS Regions and AWS China Regions
    - [x] Public docker registry to AWS ECR images copy
    - [x] Copy all images or only selected Images
    - [x] Support One-time images copy
    - [x] Support Incremental images copy

## Architecture

![](architecture.jpg)

A web portal is launched in the customer's AWS account. Through the web portal, customers can create data transfer 
tasks and manage them in a centralized place. When the user create a data transfer task through the web portal, the backend
invokes the CloudFormation API to deploy another stack to provision all resources to start data transfer. The solution 
only provision resources when needed. You can also choose to deploy the data transfer plugin independently. 

Available Plugins:
* [S3 Plugin](https://github.com/awslabs/amazon-s3-data-replication-hub-plugin)
* [ECR Plugin](https://github.com/awslabs/amazon-ecr-data-replication-hub-plugin)

## Solution Deployment

> **Time to deploy:** Approximately 15 minutes.

Refer to this [guide](../../../Downloads/data-transfer-hub-main/docs/DeployInChinaWithAuthing_EN.md) if you want deploy this solution in AWS China Regions.

### Launch CloudFormation Stack

Follow the step-by-step instructions to configure and deploy the Data Transfer Hub into your account.

1. Make sure you have sign in AWS Console already.
1. Click the following button to launch the CloudFormation Stack in your account.

    [![Launch Stack](../../../Downloads/data-transfer-hub-main/launch-stack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/create/template?stackName=DataTransferHub&templateURL=https://solutions-reference.s3.amazonaws.com/data-transfer-hub/latest/DataTransferHub-cognito.template)
1. Input **AdminEmail** parameter. An email containing the temporary password is sent to this email. You'll need access to this email to sign in.
1. Click **Next** and select **Create Stack**.

### Login into the Data Transfer Hub Portal

An email containing the temporary password will be sent to the provided email. Note the password for later use.

1. Open the CloudFormation Console, and choose the deployed stack.
1. Select the **Output** of the CloudFormation stack, and find the **PortalUrl**.
1. Open the portal in your browser.
1. Sign in with the **AdminEmail** and the temporary password.
1. Set a new password.
1. Verify your email address and turn on account recovery (optional).
1. The page redirects to the login page. 
1. Input the **AdminEmail** and the new password.

## User Manual

Create your first data transfer task, For the complete user guide, refer to
[User Guide](../../../Downloads/data-transfer-hub-main/docs/UserManual.md) for more information.

## FAQ

**Q. Which are the supported Reigons of this solution?**</br>
You can deploy this solution in these Reigons: N.Virginia (us-east-1), Ohio (us-east-2), N.California (us-west-1), 
Oregon (us-west-2), Mumbai (ap-south-1), Seoul (ap-northeast-2), Singapore (ap-southeast-1), Sydney (ap-southeast-2),
Tokyo (ap-northeast-1), Canada (ca-central-1), Frankfurt (eu-central-1), Ireland (eu-west-1), London (eu-west-2), 
Paris (eu-west-3), Stockholm (eu-north-1), São Paulo (sa-east-1), Beijing (cn-north-1), Ningxia (cn-northwest-1).

**Q. If I want to copy data from U.S. Regions to China Regions, where should I deploy the solution?**</br>
You can either deploy the solution in U.S. Regions or deploy the solution in China Regions. 

**Q. Can I deploy the solution in AWS Account A, and transfer Amazon S3 objects from Account B to Account C?**</br>
Yes. In this case, you will need to store the [AccessKeyID and SecretAccessKey](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys) 
for Account B and C in the [Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) 
of Account A.

## More Resources

* [How to customize this solution and build your own distributable?](../../../Downloads/data-transfer-hub-main/docs/build-your-own-distributable.md)
* [Deploy this solution via AWS CDK](../../../Downloads/data-transfer-hub-main/docs/deploy-via-cdk.md)