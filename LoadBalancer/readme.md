## Load Balancing
- ALB(application load balancer)*
- NLB(network load balancer)
- GLB(gateway load balancer)
- CLB(classic load balancer)


## ALB
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





