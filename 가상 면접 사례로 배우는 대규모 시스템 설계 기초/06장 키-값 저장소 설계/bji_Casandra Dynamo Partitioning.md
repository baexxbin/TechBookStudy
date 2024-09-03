## Dynamo DB

- AWS에서 제공하는 Full Managed NoSQL DB
- 다른 NoSQL과 다르게 인덱스가 존재함
- 키-값 문서형 데이터 모델을 사용
- Leader-Follower 구조를 사용하며 파티션마다 리더 노드가 있고 **리더 노드가 쓰기 작업을 처리**하고 **팔로워 노드가 읽기 작업을 처리**함
- **최종 일관성을 보장**하며 요청 시 **강한 일관성**도 선택 가능

## Casandra

- Facebook에서 Amazon의 Dynamo와 Google의 Bigtable을 참조해서 만든 NoSQL DB
- 행 기반의 분산형 NoSQL 데이터 베이스 
- **Masterless 아키텍처를 채택**하고 있으며 **모든 노드는 동일한 역할을 가지고 데이터 읽기 쓰기 작업을 처리**함
- **Consistent Hashing을 사용**하여 데이터를 분산 저장
- **다양한 일관성 수준**을 제공
  - 일관성 수준에 따라서 쓰기 성능을 튜닝할 수 있음
