
# Overview

The project is a collection of AWS Security Control Policies that can be used to control costs on accounts. 
The policies limit use of larger EC2 instance types and limit access to specified regions.

### Restrict SageMaker Studio Instance Types

This policy applies to SageMaker Studio Apps, and will limit the types of instances that can be used. 
You can customize the `sagemkaer:InstanceTypes` array in the condition property to control the allowed instance types.
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "RestrictSageMakerStudioInstanceTypes",
      "Effect": "Deny",
      "Action": [
        "sagemaker:CreateApp"
      ],
      "Condition": {
        "ForAnyValue:StringNotLike": {
          "sagemaker:InstanceTypes": [
            "default",
            "system",
            "*.medium",
            "*.large",
            "*.xlarge",
            "*.2xlarge"
          ]
        }
      },
      "Resource": [
        "*"
      ]
    }
  ]
}
```

### Restrict SageMaker Studio Notebook Instance Types

This policy restricts the instance types that may be used for SageMaker Notebooks. 
You can customize the `sagemkaer:InstanceTypes` array in the condition property to control the allowed instance types.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "RestrictSageMakerNotebookInstanceTypes",
      "Effect": "Deny",
      "Action": [
        "sagemaker:CreateNotebookInstance"
      ],
      "Resource": "*",
      "Condition": {
        "ForAnyValue:StringLike": {
          "sagemaker:InstanceTypes": [
            "u*.*",
            "z*.*",
            "i*.*",
            "h*.*",
            "d*.*",
            "x*.*",
            "*.metal",
            "*.4xlarge",
            "*.6xlarge",
            "*.8xlarge",
            "*.9xlarge",
            "*.10xlarge",
            "*.12xlarge",
            "*.16xlarge",
            "*.18xlarge",
            "*.24xlarge",
            "*.32xlarge"
          ]
        }
      }
    }
  ]
}
```

### Restrict Instance Types for Training and Processing Jobs

This policy restricts the instance types that may be used for SageMaker training and processing jobs. 
You can customize the `sagemkaer:InstanceTypes` array in the condition property to control the allowed instance types.


### 
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "RestrictSageMakerJobInstanceTypes",
      "Effect": "Deny",
      "Action": [
        "sagemaker:CreateProcessingJob",
        "sagemaker:CreateTrainingJob"
      ],
      "Resource": "*",
      "Condition": {
        "ForAnyValue:StringLike": {
          "sagemaker:InstanceTypes": [
            "u*.*",
            "z*.*",
            "i*.*",
            "h*.*",
            "d*.*",
            "x*.*",
            "*.metal",
            "*.6xlarge",
            "*.8xlarge",
            "*.9xlarge",
            "*.10xlarge",
            "*.12xlarge",
            "*.16xlarge",
            "*.18xlarge",
            "*.24xlarge",
            "*.32xlarge"
          ]
        }
      }
    }
  ]
}
```

### Restrict EC2 Instance Types

This policy restricts the instance types a user may start. 
You can customize the `ec2:InstanceType` array in the condition property to control the allowed instance types.



```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "RestrictEC2InstanceTypes",
      "Effect": "Deny",
      "Action": [
        "ec2:RunInstances"
      ],
      "Condition": {
        "ForAnyValue:StringLike": {
          "ec2:InstanceType": [
            "u*.*",
            "z*.*",
            "i*.*",
            "h*.*",
            "d*.*",
            "x*.*",
            "*.metal",
            "*.4xlarge",
            "*.6xlarge",
            "*.8xlarge",
            "*.9xlarge",
            "*.10xlarge",
            "*.12xlarge",
            "*.16xlarge",
            "*.18xlarge",
            "*.24xlarge",
            "*.32xlarge"
          ]
        }
      },
      "Resource": "arn:aws:ec2:*:*:instance/*"
    }
  ]
}
```

### Regional Access policy

This policy restricts access to AWS services to specified regions, except for an exclusion list of global services.
You can customize the `aws:RequestionRegion` array in the condition property to control the allowed regions.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowRegionAccess",
      "Effect": "Deny",
      "Condition": {
        "StringNotEquals": {
          "aws:RequestedRegion": [
            "us-east-1", 
            "eu-west-1"
          ]
        }
      },
      "NotAction": [
        "a4b:*",
        "acm:*",
        "aws-marketplace-management:*",
        "aws-marketplace:*",
        "aws-portal:*",
        "budgets:*",
        "ce:*",
        "chime:*",
        "cloudfront:*",
        "config:*",
        "cur:*",
        "ec2:DescribeRegions",
        "ec2:DescribeTransitGateways",
        "ec2:DescribeVpnGateways",
        "fms:*",
        "globalaccelerator:*",
        "health:*",
        "iam:*",
        "importexport:*",
        "kms:*",
        "mobileanalytics:*",
        "networkmanager:*",
        "organizations:*",
        "pricing:*",
        "route53:*",
        "route53domains:*",
        "s3:GetAccountPublic*",
        "s3:ListAllMyBuckets",
        "s3:PutAccountPublic*",
        "shield:*",
        "sts:*",
        "support:*",
        "trustedadvisor:*",
        "waf-regional:*",
        "waf:*",
        "wafv2:*",
        "wellarchitected:*"
      ],
      "Resource": "*"
    }
  ]
}
```