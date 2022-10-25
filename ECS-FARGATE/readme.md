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
<img width="634" alt="스크린샷 2022-10-18 오전 11 48 53" src="https://user-images.githubusercontent.com/73451727/196324192-2195c861-cba9-4cb6-976d-e795c4141674.png">



### ECS 구성 - 빠른 시작
> ### ECR 에 image push <br/>


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


> ### 테스트 <br/>
> 클러스터 -> demo-cluster -> 작업 -> public ip <br/>
> <img width="452" alt="스크린샷 2022-10-20 오후 6 12 18" src="https://user-images.githubusercontent.com/73451727/196907626-c1e896f1-2c68-47ab-ac32-6847b0ba12cc.png">


> rf) https://wooono.tistory.com/m/133 <br/>
> rf) https://www.44bits.io/ko/post/container-orchestration-101-with-docker-and-aws-elastic-container-service <br/>


### ECS 구성 2
> ### - 클러스터 생성
> <img width="789" alt="스크린샷 2022-10-24 오후 1 37 53" src="https://user-images.githubusercontent.com/73451727/197449530-9b9b1729-0091-4b0b-bb27-22a3ffc36d6f.png">
> ### - ECR 이미지 업데이트
```
FROM richarvey/nginx-php-fpm:1.5.3
RUN echo '<!DOCTYPE html><html lang="ko">' > /var/www/html/index.php ;\
    echo '<style>html{ margin: 10rem; }</style>' >> /var/www/html/index.php ;\
    echo '<h1>Nginx Demo v0.1</h1>' >> /var/www/html/index.php ;\
    echo '<h2>Hostname: <?php echo gethostname() ?></h2>' >> /var/www/html/index.php ;\
    echo '</html>' >> /var/www/html/index.php
```
<img width="614" alt="스크린샷 2022-10-24 오후 1 49 48" src="https://user-images.githubusercontent.com/73451727/197451604-041f8b87-7f28-49a0-9688-8d27d5602628.png">
<img width="640" alt="스크린샷 2022-10-24 오후 2 00 25" src="https://user-images.githubusercontent.com/73451727/197451680-76c1321f-ddad-452e-b67e-7ba7e9a4b905.png">

> ### - 테스크 데피니션 생성
<img width="663" alt="스크린샷 2022-10-24 오후 2 02 44" src="https://user-images.githubusercontent.com/73451727/197452058-0a6ac043-4dc6-490d-b720-8707a5340831.png">
<img width="652" alt="스크린샷 2022-10-24 오후 2 03 01" src="https://user-images.githubusercontent.com/73451727/197452061-201a7894-6b8f-4f6d-ba36-068fc4a12df2.png">
<img width="574" alt="스크린샷 2022-10-24 오후 2 03 40" src="https://user-images.githubusercontent.com/73451727/197452065-84a05f08-7e28-4050-b897-d862042ef910.png">

> ### - 서비스 생성 = 테스크 데피니션 선택해서 서비스 실행
<img width="451" alt="스크린샷 2022-10-24 오후 2 08 05" src="https://user-images.githubusercontent.com/73451727/197452825-e9ce2f19-12a2-43ab-aafb-7da2b510354f.png">
<img width="463" alt="스크린샷 2022-10-24 오후 2 09 18" src="https://user-images.githubusercontent.com/73451727/197452832-5ad25cc0-318a-4162-a32b-d021cdd5b174.png">
<img width="452" alt="스크린샷 2022-10-24 오후 2 10 18" src="https://user-images.githubusercontent.com/73451727/197452839-ca8cac3d-fc5e-46cc-bcec-a512d0e87915.png">
<img width="442" alt="스크린샷 2022-10-24 오후 2 10 27" src="https://user-images.githubusercontent.com/73451727/197452845-231e8cc2-70ae-4a41-8214-b71b7d6cf9f3.png">

> ### - 결과 및 테스트
<img width="696" alt="스크린샷 2022-10-24 오후 2 14 31" src="https://user-images.githubusercontent.com/73451727/197452979-ff457ba7-0b32-4c06-a0e4-b330120106d5.png">
<img width="703" alt="스크린샷 2022-10-24 오후 2 14 16" src="https://user-images.githubusercontent.com/73451727/197452992-a2f2fccd-05fb-4086-8eba-1c163de103dc.png">
<img width="711" alt="스크린샷 2022-10-24 오후 2 11 44" src="https://user-images.githubusercontent.com/73451727/197452860-c9a7e8ff-3271-42ed-8137-a07bb2f9960e.png">

> ### - 수동 배포: 서비스 업데이트 > 새 배포 적용 check > update
<img width="1355" alt="스크린샷 2022-10-25 오후 8 56 46" src="https://user-images.githubusercontent.com/73451727/197767526-be014915-1029-4389-858e-8e3a06ea7b61.png">
<img width="1588" alt="스크린샷 2022-10-25 오후 8 57 15" src="https://user-images.githubusercontent.com/73451727/197767569-90f1e246-be40-4cc7-bc83-47e66835deb9.png">
<img width="632" alt="스크린샷 2022-10-25 오후 8 57 33" src="https://user-images.githubusercontent.com/73451727/197767584-316823a8-63d4-4577-b00f-9e43573cf1da.png">
<img width="222" alt="스크린샷 2022-10-25 오후 8 57 45" src="https://user-images.githubusercontent.com/73451727/197767606-89e691e3-ec02-4b5f-817a-67e3fb12f1ca.png">

## ECS 배포
- docker-compose 는 로컬환경에서 사용하기 좋지만, production 환경에서 사용하기는 부적합함 <br/>
- docker-compose의 장점인, 여러개 컨테이너를 묶는 도커 네트워크 또한 사용하기 어려워짐 <br/>
- 그러나, aws ecs의 경우 동일한 테스크에 컨테이너를 추가하면 하나의 호스트 머신에 같이 올라감 <br/>
- 도커 네트워크 구성은 x / 단지 localhost를 사용할 수 있게 해줌 / mongodb:27017 -> localhost:27017 로 변경 <br/>
- 로컬환경 에서의 변수와 실제 배포시의 변수가 mongodb vs localhost로 갈리므로, ecr container 추가시에 variables를 추가로 설정한다 <br/>
- MONGODB_URL = localhost <br/>
- 도커화된 앱을 배포할 때는, 도커 네트워크를 사용할 수 없음(즉, 컨테이너 이름 자체로 다른 컨테이너에 접근하는것이 불가능해짐) <br/>
