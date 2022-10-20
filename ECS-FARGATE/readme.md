#### ECS의 구성요소 4가지: 클러스터 / 컨테이너 / 테스크 / 서비스
<img width="560" alt="스크린샷 2022-10-20 오후 4 40 15" src="https://user-images.githubusercontent.com/73451727/196886744-b000e9e3-3432-452d-ac68-ec42efc3a5db.png">


> rf) https://wooono.tistory.com/m/133 <br/>
> AWS의 ECS는 Amazon에서 제공하는 '완전관리형 컨테이너 오케스트레이션 툴'로써, <br/>
> Docker 컨테이너를 이용하여 인프라 환경을 좀 더 편리하게 운영,관리 할 수 있게 해주는 서비스이다. <br/>
> 비슷한 툴로서는 Kubernetes나 Docker Swarm이 있다. <br/>
> - ECS의 구성요소 <br/>
>> - Task definition: 원하는 Docker 컨테이너를 생성할 때, 어떤 설정으로 몇 개 이상 생성 할 지를 정의한 Set 이다. <br/>
>> -  Task: Task definition 에서 정의된 대로 배포된 Container Set을 Task라고 부른다. <br/>
>> -  Service: Task 들의 Life cycle 을 관리하는 부분을 Service 라고 한다. <br/>
>> -  Container Instance: EC2 or fargate <br/>
>> -  Cluster: Task 가 배포되는 Container Instance 들은 논리적인 그룹으로 묶이게 되는데 이 단위를 Cluster 라고 부른다. <br/>
<img width="634" alt="스크린샷 2022-10-18 오전 11 48 53" src="https://user-images.githubusercontent.com/73451727/196324192-2195c861-cba9-4cb6-976d-e795c4141674.png">


#### - ECS는 컨테이너 배포형식으로 EC2 와 fargate(serverless)를 사용할수 있다.
> <img width="897" alt="스크린샷 2022-10-18 오전 11 28 51" src="https://user-images.githubusercontent.com/73451727/196321407-78027adf-9637-4bae-b8d7-f00bff5bd86f.png">



## 1. 클러스터 생성
## 2. 서비스 생성
## 3. 작업정의 생성
