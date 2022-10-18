# terraform
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
  
