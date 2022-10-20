## Load Balancing
- ALB(application load balancer)*
- NLB(network load balancer)
- GLB(gateway load balancer)
- CLB(classic load balancer)


## ALB
vpc -> alb -> targetgroup -> instance
<img width="693" alt="스크린샷 2022-10-19 오후 6 35 40" src="https://user-images.githubusercontent.com/73451727/196655044-e0c96eb2-8fc7-4e55-bfc4-fa6566b8f3ca.png">

- scale out방식으로 여러대의 서버를 하나의 도메인으로 사용할수 있게해줌
- 패스나 포트등에 따라 다른 대상그룹으로 맵핑할 수 있다.
- 특히, 포트단위로 연결해줄수 있을경우 도커컨테이너 환경에 유리
- 하나의 대상그룹에 더 많은 컨테이너를 넣어 비용을 최적화 할 수 있다.
- 대상을 EC2 / 람다 / IP로도 연결이 가능하며, 서버없이 직접 응답메세지를 작성할수도 있다.
- MSA 아키텍쳐를 구성하기에 좋음

## 타켓그룹/리스너/룰
<img width="692" alt="스크린샷 2022-10-19 오후 6 40 06" src="https://user-images.githubusercontent.com/73451727/196656127-f226f3d1-4cb7-4641-bf86-fe3d68848121.png">

- 각 리스너 규칙을 생성할 때 대상 그룹 및 조건을 지정합니다. 
- 규칙 조건이 충족되면 해당하는 대상 그룹으로 트래픽이 전달됩니다. 
- 서로 다른 유형의 요청에 대해 서로 다른 대상 그룹을 생성할 수 있습니다.

## ALB 구성

### 1. ALB + EC2 두개 구성
rf) https://cloudest.tistory.com/31 <br/>

#### - 요구사항
  > ALB를 생성하여 HTTP로 접근하는 웹서버에 대한 로드밸런싱 환경을 만든다. <br/>
  > 여러개의 서버를 하나의 DNS 주소로 제공할 수 있다. <br/>
  
#### - EC2 두개 생성 -> docker-fastapi 환경 구성 -> 80번 포트 open + /api/health check 처리
```
from fastapi import FastAPI
app = FastAPI()
@app.get("/")
async def root():
    return {"message": "hello world dockerized fast api !!"}

@app.get("/api/health")
async def root():
    return 1
```

#### - 대상그룹 생성 및 생성된 EC2 register
<img width="825" alt="스크린샷 2022-10-20 오후 3 26 54" src="https://user-images.githubusercontent.com/73451727/196872390-e82ba031-8439-4e91-9b53-f610b98f9fb1.png">
<img width="647" alt="스크린샷 2022-10-20 오후 3 27 14" src="https://user-images.githubusercontent.com/73451727/196872413-af372d22-6d27-4d42-9bdf-f836b652f85c.png">
<img width="1745" alt="스크린샷 2022-10-20 오후 3 27 57" src="https://user-images.githubusercontent.com/73451727/196872546-67d60f26-003a-4fba-86ba-fe3735de7cac.png">

-  로드밸런스 생성 및 HTTP 80 리스너에 대상그룹 추가 (보안그룹 80번 포트 오픈되어있는지 확인*)
<img width="765" alt="스크린샷 2022-10-20 오후 3 29 07" src="https://user-images.githubusercontent.com/73451727/196873199-ac93ac8d-426d-4e5a-b6aa-5839f0d757fe.png">
<img width="745" alt="스크린샷 2022-10-20 오후 3 30 23" src="https://user-images.githubusercontent.com/73451727/196873218-33ba5fae-d1a3-48c5-a4e6-74f4f9846368.png">
<img width="733" alt="스크린샷 2022-10-20 오후 3 30 37" src="https://user-images.githubusercontent.com/73451727/196873248-d24e31e8-8aac-46cb-ae29-5f8ecbc60262.png">
<img width="729" alt="스크린샷 2022-10-20 오후 3 31 17" src="https://user-images.githubusercontent.com/73451727/196873270-ee94d23a-dc83-4dbe-800f-9895daa59933.png">

#### - 테스트
  > 로드벨런서 DNS로 접속
  > 접속시 EC2 두개에 번갈아가면서 접속됨
 <img width="736" alt="스크린샷 2022-10-20 오후 3 34 08" src="https://user-images.githubusercontent.com/73451727/196873684-a825e962-3eff-4024-a6d5-bc14e981ccb1.png">
<img width="689" alt="스크린샷 2022-10-20 오후 3 17 48" src="https://user-images.githubusercontent.com/73451727/196873706-d03c0902-b9b2-4c06-9dbe-095025ae192f.png">
<img width="621" alt="스크린샷 2022-10-20 오후 3 17 58" src="https://user-images.githubusercontent.com/73451727/196873725-69029235-117d-4651-9ee1-839a680deb32.png">






