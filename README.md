# Fullstack React + Node.js + PostgreSQL on AWS (CloudFormation)

This AWS CloudFormation template automates the deployment of a fullstack web application that includes:

- **React** frontend
- **Node.js** backend (Express)
- **PostgreSQL** database
- **Nginx** reverse proxy
- **Private and public EC2 instances**
- **NAT Gateway setup for private networking**

## Architecture Overview

- A **VPC** with both **public** and **private subnets**
- A **public EC2 instance** running **Nginx** as a reverse proxy
- A **private EC2 instance** hosting the fullstack app (Node.js, React, PostgreSQL)
- A **NAT Gateway** for internet access from the private instance
- **Security Groups** for controlled access to ports
- PostgreSQL is only accessible within the private subnet

## Prerequisites

- An AWS account with access to create EC2, VPC, and related resources
- A valid EC2 **Key Pair** in the region where you deploy this template
- (Optional) AWS CLI or CloudFormation Console to launch the stack

## Parameters

| Parameter      | Description                         | Default         |
|----------------|-------------------------------------|-----------------|
| `KeyName`      | Name of an existing EC2 Key Pair    | (required)      |
| `InstanceType` | EC2 instance type                   | `t3.micro`      |
| `DBName`       | PostgreSQL database name            | `fullstackdb`   |
| `DBUser`       | PostgreSQL username                 | `fullstack`     |
| `DBPassword`   | PostgreSQL user password            | `react@123`     |

## How to Deploy

### 1. Launch with AWS Console

1. Open the [AWS CloudFormation Console](https://console.aws.amazon.com/cloudformation/home).
2. Choose **Create Stack** → **With new resources (standard)**.
3. Upload the CloudFormation YAML file or paste the content.
4. Fill in the parameters.
5. Click **Next** and follow the wizard to deploy.

### 2. Deploy via AWS CLI

```bash
aws cloudformation create-stack \
  --stack-name fullstack-react-app \
  --template-body file://template.yaml \
  --parameters \
    ParameterKey=KeyName,ParameterValue=your-key-name \
    ParameterKey=DBPassword,ParameterValue=your-db-password \
  --capabilities CAPABILITY_NAMED_IAM
