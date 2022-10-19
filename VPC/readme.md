## VPC / CIDR
- 배경
  > ipv4의 숫자가 충분치않음 <br/>
  > ip address를 아껴써보자 -> 하나의 public ip를 여러 기기가 공유 -> 사설망 <br/>
  > 하나의 사설망에는 private ip를 부여받은 기기들과 gateway로 구성 <br/>
  > 각 기기는 인터넷과 통신시 gateway를 통해 통신 <br/>
  > 사설망은 아래와 같이 3개의 대역이 미리 정의되어있음 <br/>
<img width="1588" alt="스크린샷 2022-10-18 오후 5 59 01" src="https://user-images.githubusercontent.com/73451727/196385753-32daf689-284b-45fe-8945-7c534f587d11.png">
<img width="643" alt="스크린샷 2022-10-18 오후 6 31 56" src="https://user-images.githubusercontent.com/73451727/196393507-fff61f9f-6e35-42cb-b0b9-46d342ab4091.png">
<img width="803" alt="스크린샷 2022-10-18 오후 6 10 49" src="https://user-images.githubusercontent.com/73451727/196388517-2f8f8215-af98-4d1b-83a2-723ab22e0799.png">

- VPC란? 
  > virtual private network 즉, 데이터센터와 유사한 가상 사설망

- CIDR란?
  > 여러개의 사설망을 구축하기 위해 망을 나누는 방법 <br/>
  > Classless Inter Domain Routing <br/>
  > Classless vs Classful <br/>
  > 전통적으로 네트워크비트를 8/16/24로 클래스화시키는 classful 서브네팅을 더욱 유연하게 만듬 <br/>
  > 즉, 필요한만큼 가변적으로 네트워크 비트 세팅이 가능함 (22,23,25,26 등등) <br/>
<img width="854" alt="스크린샷 2022-10-18 오후<img width="650" alt="스크린샷 2022-10-19 오전 11 58 29" src="https://user-images.githubusercontent.com/73451727/196586907-8bf79b90-e3b7-4254-ae26-e3a3e47da0ed.png">
 6 31 41" src="https://user-images.githubusercontent.com/73451727/196393554-63cf49e0-d895-4b79-aeb1-4325fc7b0f47.png">

- IPv4 CIDR BLOCK
  > VPC 내의 인스턴스 및 리소스에 할당되는 IP 주소를 결정 <br/>
  > 일반적으로 아래 3개중 하나를 설정한다. <br/>
  > 10.0.0.0/8 [16777216-5(aws기준)의 갯수만큼 호스트를 가질수 있다.] <br/>
  > 172.16.0.0/12 [104857-5(aws기준)의 갯수만큼 호스트를 가질수 있다.] <br/>
  > 192.168.0.0/16 [65536-5(aws기준)의 갯수만큼 호스트를 가질수 있다.] <br/>
<img width="643" alt="스크린샷 2022-10-18 오후 6 48 48" src="https://user-images.githubusercontent.com/73451727/196397418-86647ea3-603e-4451-a27d-614037e11ffa.png">

## VPC 구성
<img width="608" alt="스크린샷 2022-10-19 오후 12 22 59" src="https://user-images.githubusercontent.com/73451727/196590258-43930230-619c-4dc9-8b8c-ff1351e85c85.png">

#### 1. VPC 생성
- ecs-test-vpc
<img width="650" alt="스크린샷 2022-10-19 오전 11 58 29" src="https://user-images.githubusercontent.com/73451727/196586925-bb3517cd-8d0a-4115-8bd7-29779ee9bf0e.png">

#### 2. 서브넷 생성 (public / private)
- ecs-test-public-subnet-01
- ecs-test-private-subnet-01

<img width="664" alt="스크린샷 2022-10-19 오후 12 00 10" src="https://user-images.githubusercontent.com/73451727/196587227-ce2fa515-2d93-4d1f-adef-0da739430583.png">
<img width="648" alt="스크린샷 2022-10-19 오후 12 00 49" src="https://user-images.githubusercontent.com/73451727/196587237-80effd2d-b5fa-4e88-a56b-b72a2533300a.png">

#### 3. IGW 생성
<img width="670" alt="스크린샷 2022-10-19 오후 12 01 46" src="https://user-images.githubusercontent.com/73451727/196587577-95b02072-d838-4557-982b-2185e9c34146.png">
<img width="1528" alt="스크린샷 2022-10-19 오후 12 02 12" src="https://user-images.githubusercontent.com/73451727/196587540-30d17e07-4761-4555-9fd1-478f79afad7f.png">
<img width="662" alt="스크린샷 2022-10-19 오후 12 02 38" src="https://user-images.githubusercontent.com/73451727/196587484-9b0c06da-ccb1-402f-b5a3-c8360d75c970.png">

#### 4. 라우팅 테이블 정의
- ecs-test-public-route 
  > 라우팅테이블 생성
  > 라우팅 편집 -> 추가 0.0.0.0/0 - igw
  > 서브넷 연결 ecs-test-public-subnet-01
- ecs-test-private-route
  > 라우팅테이블 생성
  > 서브넷 연결 ecs-test-private-subnet-01

<br/>

- default route table: destination: 192.168.0.0/16 target: local
- VPC 범위의 IP로 향하는 모든 트래픽이 local로 라우팅 된다.
- 즉, VPC 내 모든 서브넷이 서로 통신할 수 있다는 것을 의미한다.
- rf) https://suyeon96.tistory.com/m/45

<img width="657" alt="스크린샷 2022-10-19 오후 12 07 33" src="https://user-images.githubusercontent.com/73451727/196588612-0ae66fcb-6b27-4ed0-a376-1ff3f32e68c7.png">
<img width="1525" alt="스크린샷 2022-10-19 오후 12 08 05" src="https://user-images.githubusercontent.com/73451727/196588610-94119f85-393b-4649-87c2-e7f22b42ec55.png">
<img width="1751" alt="스크린샷 2022-10-19 오후 12 08 28" src="https://user-images.githubusercontent.com/73451727/196588608-31b6d0d9-a6b0-447d-94c2-a109a7b5d7cc.png">
<img width="1508" alt="스크린샷 2022-10-19 오후 12 08 49" src="https://user-images.githubusercontent.com/73451727/196588607-0315f6d9-c3c7-49cd-af94-76f5ee4ae41a.png">
<img width="1741" alt="스크린샷 2022-10-19 오후 12 09 12" src="https://user-images.githubusercontent.com/73451727/196588604-7aae16cd-6936-4d48-b4d1-59f7e36a628f.png">
<img width="663" alt="스크린샷 2022-10-19 오후 12 09 41" src="https://user-images.githubusercontent.com/73451727/196588601-c47eb533-d5bb-4962-b1e9-5a8ead5104ae.png">
<img width="1524" alt="스크린샷 2022-10-19 오후 12 10 03" src="https://user-images.githubusercontent.com/73451727/196588600-9444b533-7d67-4fd1-b024-9554e1ec6d09.png">
<img width="1746" alt="스크린샷 2022-10-19 오후 12 10 17" src="https://user-images.githubusercontent.com/73451727/196588596-cb183f7f-dc37-4573-b146-88006893eaa8.png">
