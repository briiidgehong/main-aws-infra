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
<img width="854" alt="스크린샷 2022-10-18 오후 6 31 41" src="https://user-images.githubusercontent.com/73451727/196393554-63cf49e0-d895-4b79-aeb1-4325fc7b0f47.png">

  > 여러개의 사설망을 구축하기 위해 망을 나누는 방법 <br/>
  > Classless Inter Domain Routing <br/>
  > Classless vs Classful <br/>
  > 전통적으로 네트워크비트를 8/16/24로 클래스화시키는 classful 서브네팅을 더욱 유연하게 만듬 <br/>
  > 즉, 필요한만큼 가변적으로 네트워크 비트 세팅이 가능함 (22,23,25,26 등등) <br/>

- IPv4 CIDR BLOCK
  > VPC 내의 인스턴스 및 리소스에 할당되는 IP 주소를 결정 <br/>
  > 10.0.0.0/8 , 172.16.0.0/12 , 192.168.0.0/16 <br/>

## SUBNET 
- 퍼블릭, 프라이빗 서브넷으로 구성 <br/>
- 서브넷은 라우트 테이블에 연결되어있는 구조 <br/>
- 라우트 테이블 구성시에 0.0.0.0/0 즉, 외부로 나가는 트래픽이 IGW이면 퍼블릭 서브넷 NAT이면 프라이빗 서브넷이다. <br/>
## igw, nat gateway 
## route table
