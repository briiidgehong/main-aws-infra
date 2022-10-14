## EC2
<img width="1535" alt="스크린샷 2022-10-14 오후 2 44 16" src="https://user-images.githubusercontent.com/73451727/195772358-8b830022-679e-46d3-bf76-6e7832713d21.png">
<img width="540" alt="스크린샷 2022-10-14 오후 2 45 33" src="https://user-images.githubusercontent.com/73451727/195772372-40f571e4-0354-473a-b107-ec2aecaf084e.png">
<img width="1904" alt="스크린샷 2022-10-14 오후 2 45 25" src="https://user-images.githubusercontent.com/73451727/195772392-17106ac7-8eb6-42ca-b839-07f6dfd7fadd.png">



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
  
