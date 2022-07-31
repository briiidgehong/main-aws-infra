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
  bucket = "terraform101-inflearn"
}
```

- terraform init
- terraform plan
- terraform apply

2. vpc / subnet / igw, nat gateway / route table
