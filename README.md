## AWS
### - [VPC-CIDR](https://github.com/briiidgehong/main-aws-terraform/tree/main/VPC-CIDR)
### - [EC2](https://github.com/briiidgehong/main-aws-terraform/tree/main/EC2)
### - [LoadBalancer](https://github.com/briiidgehong/main-aws-terraform/tree/main/LoadBalancer)
### - [ElasticBeanstalk](https://github.com/briiidgehong/main-aws-terraform/tree/main/ElasticBeanstalk)
### - [ECS-FARGATE](https://github.com/briiidgehong/main-aws-terraform/tree/main/ECS-FARGATE)
### - []()


## terraform
iac, terraform


1. s3 bucket 생성
  - provider.tf
  ```
  provider "aws" {
    region = "ap-northeast-2"
  }
  ```

  - s3.tf
  ```
  resource "aws_s3_bucket" "test" {
    bucket = "jyhong-private-s3"
  }
  ```

  - terraform init
  - terraform plan
  - terraform apply
  
