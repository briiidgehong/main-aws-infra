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

2. vpc / subnet / igw, nat gateway / route table
  2-1. vpc
    - create vpc
      - name tag: terraform-test-vpc
      - IPv4 CIDR block :
        - 10.0.0.0/8 , 172.16.0.0 , 192.168.0.0/16
        - VPC 내의 인스턴스 및 리소스에 할당되는 IP 주소를 결정
  2-2. subnet 
    - 퍼블릭, 프라이빗 서브넷으로 구성
    - 서브넷은 라우트 테이블에 연결되어있는 구조
    - 라우트 테이블 구성시에 0.0.0.0/0 즉, 외부로 나가는 트래픽이 IGW이면 퍼블릭 서브넷 NAT이면 프라이빗 서브넷이다.
  
