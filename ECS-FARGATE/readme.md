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
```
# create dockerfile
mkdir dockerized-fast-api
sudo vi Dockerfile / main.py / requirements.txt

- dockerfile
FROM python:3.7
USER root
WORKDIR /app/
COPY ./requirements.txt /app/requirements.txt
RUN pip install -r /app/requirements.txt 
COPY . /app/
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]

- main.py
from fastapi import FastAPI
app = FastAPI()
@app.get("/")
async def root():
    return {"message": "hello world dockerized fast api !!"}
    
- requirements.txt
anyio==3.6.1
click==8.1.3
fastapi==0.85.0
h11==0.14.0
httptools==0.5.0
idna==3.4
importlib-metadata==5.0.0
pydantic==1.10.2
python-dotenv==0.21.0
PyYAML==6.0
sniffio==1.3.0
starlette==0.20.4
typing_extensions==4.4.0
uvicorn==0.18.3
uvloop==0.17.0
watchfiles==0.17.0
websockets==10.3
zipp==3.9.0


Docker build —t “dockerized-fast-api-image” .
sudo docker build -t dockerized-fast-api-image .
```
> public repository / port 80:80 <br/>
<img width="881" alt="스크린샷 2022-10-21 오후 5 04 22" src="https://user-images.githubusercontent.com/73451727/197145411-c3b21bf8-67e3-4c54-b288-223b7fce34c2.png">
<img width="616" alt="스크린샷 2022-10-21 오후 5 04 06" src="https://user-images.githubusercontent.com/73451727/197145434-53dfbb43-a777-44ce-9731-ed485d85e72c.png">
<br/>

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


## ECS 구성 - ALB / auto scailing 적용
### - 1. ECR 이미지 업로드 - 위의 ecr image 사용
### - 2. 클러스터 생성
### - 3. 테스트 데피니션 생성
### - 4. 서비스 생성 = 테스크 데피니션 맵핑 및 서비스 실행
### - 5. 결과 및 테스트
### - 6. 수동 배포: 서비스 업데이트 > 새배포적용 check > 업데이트
<br/>

> ### - 2. 클러스터 생성
<br/>
<img width="794" alt="스크린샷 2022-10-26 오후 10 02 53" src="https://user-images.githubusercontent.com/73451727/198033100-d0730d4b-7c56-4fc3-85d9-e8347f65caee.png">
<img width="644" alt="스크린샷 2022-10-26 오후 10 04 09" src="https://user-images.githubusercontent.com/73451727/198033128-08b0487b-c40d-4bac-a396-282359fc49aa.png">

> ### - 3. 테스크 데피니션 생성
<br/>
<img width="932" alt="스크린샷 2022-10-26 오후 10 05 06" src="https://user-images.githubusercontent.com/73451727/198033618-82972562-deb0-498a-a12b-b7e3a40fe34d.png">
<img width="459" alt="스크린샷 2022-10-26 오후 10 08 04" src="https://user-images.githubusercontent.com/73451727/198033964-59969fbe-9e9f-4273-9052-665a3e32117b.png">
<img width="451" alt="스크린샷 2022-10-26 오후 10 08 31" src="https://user-images.githubusercontent.com/73451727/198034079-a9fb8fc2-7e39-4bc1-b930-d2cc4e36c7fa.png">
<img width="589" alt="스크린샷 2022-10-26 오후 10 16 14" src="https://user-images.githubusercontent.com/73451727/198035752-64fb95dc-ed19-4545-bf8b-c1ac07eb8cce.png">

> ### - 4. 서비스 생성 = 테스크 데피니션 맵핑 및 서비스 실행
<br/>
<img width="440" alt="스크린샷 2022-10-26 오후 10 20 15" src="https://user-images.githubusercontent.com/73451727/198036706-bd490c00-49fc-4ccd-939d-535bb72fa9f7.png">
<img width="447" alt="스크린샷 2022-10-26 오후 10 21 59" src="https://user-images.githubusercontent.com/73451727/198037051-023b2af9-71dd-47ca-a0b9-d0fee6b7b428.png">
<img width="589" alt="스크린샷 2022-10-26 오후 10 21 11" src="https://user-images.githubusercontent.com/73451727/198037075-f971c63f-431a-43ee-9b77-37e43da36044.png">

- 로드밸런서 생성 <br/>
<img width="752" alt="스크린샷 2022-10-26 오후 10 24 50" src="https://user-images.githubusercontent.com/73451727/198037851-f05129a6-d828-4dfd-abf4-fddc331385e3.png">
<img width="525" alt="스크린샷 2022-10-26 오후 10 24 56" src="https://user-images.githubusercontent.com/73451727/198037865-3ebc7f15-f527-4229-9222-f68051f3f225.png">
<img width="553" alt="스크린샷 2022-10-26 오후 10 28 22" src="https://user-images.githubusercontent.com/73451727/198038481-3a92ddfb-4b71-4d6f-b819-bfcb85069848.png">
<img width="850" alt="스크린샷 2022-10-26 오후 10 30 26" src="https://user-images.githubusercontent.com/73451727/198038951-6ca35267-7376-4627-93e9-da9bf6b59d5f.png">

> - create target group <br/>
> <img width="554" alt="스크린샷 2022-10-26 오후 10 37 46" src="https://user-images.githubusercontent.com/73451727/198040920-06aa45dc-f06e-4dd0-8e87-5b8668e547a0.png"> <br/>
> - target group 인스턴스 지정은 따로 안해도 됨 > ECS 에서 실행할때 자동으로 등록해줌 <br/>
> <img width="547" alt="스크린샷 2022-10-26 오후 10 42 17" src="https://user-images.githubusercontent.com/73451727/198042008-7b0f2cc5-e70b-44fc-aa45-85ce7d8e0f72.png"> <br/>

- 다시 서비스 생성으로 돌아와서 <br/>
<img width="379" alt="스크린샷 2022-10-26 오후 10 46 15" src="https://user-images.githubusercontent.com/73451727/198043042-4f5c1cd1-c333-4e6d-be89-016fc26fe657.png">
<img width="449" alt="스크린샷 2022-10-26 오후 10 50 14" src="https://user-images.githubusercontent.com/73451727/198044038-06e4dd55-7b05-4cfa-a27a-33246b1e293d.png">
<img width="457" alt="스크린샷 2022-10-26 오후 10 50 38" src="https://user-images.githubusercontent.com/73451727/198044137-85527002-aea3-4dd8-b6eb-c51fc2ee7ffe.png">

> ### - 5. 결과 및 테스트
<br/>
- task public ip 접속 <br/>
<img width="766" alt="스크린샷 2022-10-26 오후 10 51 46" src="https://user-images.githubusercontent.com/73451727/198044485-0ffb5508-0f73-4ab7-a405-db9812596586.png">
<img width="765" alt="스크린샷 2022-10-26 오후 10 52 18" src="https://user-images.githubusercontent.com/73451727/198044611-4a7271c6-9b61-46ee-87ec-eec239e55b89.png">
<img width="426" alt="스크린샷 2022-10-26 오후 10 52 31" src="https://user-images.githubusercontent.com/73451727/198044635-018e7d37-c3d2-43d4-bcbb-549adeccea94.png">

- ALB DNS 접속 <br/>
<img width="732" alt="스크린샷 2022-10-26 오후 10 54 02" src="https://user-images.githubusercontent.com/73451727/198045205-cde0ac15-77ee-43c5-9792-558f6b4a7fe9.png">
<img width="753" alt="스크린샷 2022-10-26 오후 10 54 22" src="https://user-images.githubusercontent.com/73451727/198045250-7b67abcc-8204-4cdd-a9cd-34e2e659ebac.png">



> ### - 6. 수동 배포: 서비스 업데이트 > 새배포적용 check > 업데이트
<br/>


## ECS 배포 추가사항
- 일반적으로 docker-compose 는 로컬환경에서 사용하기 좋지만, production 환경에서 사용하기는 부적합함 <br/>
- docker-compose의 장점인, 여러개 컨테이너를 묶는 도커 네트워크 또한 사용하기 어려워짐 <br/>
- 그러나, aws ecs의 경우 동일한 테스크에 컨테이너를 추가하면 하나의 호스트 머신에 같이 올라감 <br/>
- 도커 네트워크 구성은 x / 단지 localhost를 사용할 수 있게 해줌 / mongodb:27017 -> localhost:27017 로 변경 <br/>
- 로컬환경 에서의 변수와 실제 배포시의 변수가 mongodb vs localhost <br/>
- ecr container 추가시에 variables를 추가로 설정한다 <br/>
- MONGODB_URL = localhost <br/>
- 도커화된 앱을 배포할 때는, 도커 네트워크를 사용할 수 없음(즉, 컨테이너 이름 자체로 다른 컨테이너에 접근하는것이 불가능해짐) <br/>
<br/>

- local에서처럼 db 볼륨을 이용하는 방법 -> EFS (elastic file system) <br/>
- 보안그룹설정 및 container edit -> storage 설정 필요 <br/>
- 롤링 배포시, 현재 컨테이너와 배포하려는 컨테이너가 동시에 EFS 접근하여 충돌함 - RDS와 같은 관리형 DB를 쓰자. <br/>
<br/>

