## ECS
> AWS의 ECS는 Amazon에서 제공하는 '완전관리형 컨테이너 오케스트레이션 툴'로써, <br/>
> Docker 컨테이너를 이용하여 인프라 환경을 좀 더 편리하게 운영,관리 할 수 있게 해주는 서비스이다. <br/>
> 비슷한 툴로서는 Kubernetes나 Docker Swarm이 있다. <br/>

<img width="560" alt="스크린샷 2022-10-20 오후 4 40 15" src="https://user-images.githubusercontent.com/73451727/196886744-b000e9e3-3432-452d-ac68-ec42efc3a5db.png">

### ECS는 컨테이너 배포형식으로 EC2 와 fargate(serverless)를 사용할수 있다.
> <img width="897" alt="스크린샷 2022-10-18 오전 11 28 51" src="https://user-images.githubusercontent.com/73451727/196321407-78027adf-9637-4bae-b8d7-f00bff5bd86f.png">

### 구성요소 : 클러스터/테스크/테스크데피니션/서비스
#### 클러스터
```
도커 컨테이너를 실행할 수 있는 가상의 공간
컴퓨팅자원을 기본적으로 포함하고 있지 않은 논리적인 단위
```
#### 테스크
```
컨테이너를 실행하는 최소 단위
하나 이상의 컨테이너로 구성됨
```
#### 테스크 데피니션
```
테스크를 실행할 때 필요한 정의 (도커이미지/네트워크모드/실행명령어/CPU,메모리 제한 등)
컨테이너 오케스트레이션에서는 컨테이너가 필요에 따라 자동으로 실행되거나 종료될 수 있다.
따라서, 이러한 설정을 매번 지정하기보다는 미리 설정의 집합을 생성해놓는것이 효울적 -> 테스크 데피니션
테스크는 클러스터에 종속적이지만, 테스크 데피니션은 클러스터에 종속적이지 않음*
```
#### 서비스
```
테스크를 실행하는 방법
보통의 경우, 테스크 데피니션을 직접 실행하는 방식은 거의 쓰지 않고 서비스를 정의해서 서비스가 테스크 데피니션을 실행하게 함
서비스는 하나의 테스크 데피니션과 연결
클러스터 내에서 테스크를 스케쥴링하는 역할
```
<img width="452" alt="스크린샷 2022-10-20 오후 6 12 18" src="https://user-images.githubusercontent.com/73451727/196907626-c1e896f1-2c68-47ab-ac32-6847b0ba12cc.png">

> ### 컨테이너(컨테이너 정의) <br/>
> <img width="659" alt="스크린샷 2022-10-20 오후 5 54 10" src="https://user-images.githubusercontent.com/73451727/196903549-a933116b-b9e7-4ffc-b7d8-65927743b4ca.png">
> <img width="585" alt="스크린샷 2022-10-20 오후 5 54 31" src="https://user-images.githubusercontent.com/73451727/196903577-7c37efbf-447a-4244-94b5-27e0bcfca452.png">


> ### 테스크(테스트 정의) <br/>
><img width="655" alt="스크린샷 2022-10-20 오후 5 55 53" src="https://user-images.githubusercontent.com/73451727/196903972-63889b48-f312-4e14-95dd-429614eb69b1.png">


> ### 서비스 <br/>
><img width="661" alt="스크린샷 2022-10-20 오후 5 57 13" src="https://user-images.githubusercontent.com/73451727/196904211-3aac5cb3-59e3-46b1-9a4e-fa22146d95b9.png">
><img width="587" alt="스크린샷 2022-10-20 오후 5 57 28" src="https://user-images.githubusercontent.com/73451727/196904220-bca52c10-8253-4d2d-922f-b8a3076825d0.png">

> ### 클러스터 <br/>
><img width="642" alt="스크린샷 2022-10-20 오후 6 00 23" src="https://user-images.githubusercontent.com/73451727/196904817-cdf46dec-c939-48db-9667-99f5c7c30910.png">



<img width="634" alt="스크린샷 2022-10-18 오전 11 48 53" src="https://user-images.githubusercontent.com/73451727/196324192-2195c861-cba9-4cb6-976d-e795c4141674.png">

> rf) https://wooono.tistory.com/m/133 <br/>

### ECS 구성 - single container
#### 1. ECR 에 image push
#### 2. 컨테이너 정의
#### 2. 테스트 정의
#### 3. 서비스
#### 5. 클러스터
#### 테스트
- 클러스터 -> demo-cluster -> 작업 -> public ip

