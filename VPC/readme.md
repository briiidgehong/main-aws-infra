## VPC / CIDR
- create vpc
- name tag: test-vpc
- IPv4 CIDR BLOCK
  > VPC 내의 인스턴스 및 리소스에 할당되는 IP 주소를 결정 <br/>
  > 10.0.0.0/8 , 172.16.0.0 , 192.168.0.0/16 <br/>

## SUBNET 
- 퍼블릭, 프라이빗 서브넷으로 구성 <br/>
- 서브넷은 라우트 테이블에 연결되어있는 구조 <br/>
- 라우트 테이블 구성시에 0.0.0.0/0 즉, 외부로 나가는 트래픽이 IGW이면 퍼블릭 서브넷 NAT이면 프라이빗 서브넷이다. <br/>
## igw, nat gateway 
## route table
