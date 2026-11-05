## Designing Data-Intensive Applications

- Martin Kleppmann, 2017년 초판 요약
- 기준 원문: [Book-2Designing-data-intensive-applications.pdf](./Book-2Designing-data-intensive-applications.pdf), 총 613쪽
- 12개 장과 원문 목차의 각 절을 장별 README에 정리함. 영문 절 제목을 유지하고 한국어 설명을 붙임
- 항공기·부품·정비 기록은 이해를 위한 비유임. 원문 사례 및 실제 정비 절차와 구분함
- 제품 사례는 출간 당시의 맥락임. 변경된 기능·버전별 보장은 해당 절의 공식 문서 주석을 함께 확인함
- 범위와 검증 결과: [REVIEW.md](./REVIEW.md)

<br>

### Part I. Foundations of Data Systems — 저장과 변경의 기초

| 장 | 핵심 질문 | 정비 비유 |
| --- | --- | --- |
| [01. 신뢰성·확장성·유지보수성](./%5B01%5D%20Reliable,%20Scalable,%20and%20Maintainable%20Applications/README.md) | 고장·부하·변경에 어떻게 대응하는가 | 고장 격리, 작업량 증가, 인수인계 |
| [02. 데이터 모델과 질의](./%5B02%5D%20Data%20Models%20and%20Query%20Languages/README.md) | 무엇을 묶고 어떻게 연결·조회하는가 | 기체·부품·장탈착 이력의 관계 |
| [03. 저장과 검색](./%5B03%5D%20Storage%20and%20Retrieval/README.md) | 저장·검색 비용을 어떻게 나누는가 | 원본 기록과 조회용 색인 |
| [04. 데이터 형식과 호환성](./%5B04%5D%20Encoding%20and%20Evolution/README.md) | 양식이 바뀌어도 서로 읽을 수 있는가 | 개정 전후 양식과 과거 기록 호환 |

<br>

### Part II. Distributed Data — 여러 장비의 기록 맞추기

| 장 | 핵심 질문 | 정비 비유 |
| --- | --- | --- |
| [05. 복제](./%5B05%5D%20Replication/README.md) | 사본을 어떻게 갱신하고 충돌을 푸는가 | 여러 기지의 기록 사본과 전달 지연 |
| [06. 분할](./%5B06%5D%20Partitioning/README.md) | 데이터·작업량을 어떻게 나누는가 | 기록 분담과 담당 위치 추적 |
| [07. 트랜잭션](./%5B07%5D%20Transactions/README.md) | 일부 반영·동시 수정의 오류를 어떻게 막는가 | 작업 이력과 현재 현황을 함께 변경 |
| [08. 분산 시스템의 실패](./%5B08%5D%20The%20Trouble%20with%20Distributed%20Systems/README.md) | 응답·시각·권한을 어디까지 믿는가 | 회신 유실과 지연된 작업 지시 |
| [09. 일관성과 합의](./%5B09%5D%20Consistency%20and%20Consensus/README.md) | 최신성·순서·결정을 어떻게 보장하는가 | 같은 자원의 권한과 최종 상태 확정 |

<br>

### Part III. Derived Data — 원본에서 현황·분석 결과 만들기

| 장 | 핵심 질문 | 정비 비유 |
| --- | --- | --- |
| [10. 일괄 처리](./%5B10%5D%20Batch%20Processing/README.md) | 고정 입력을 어떻게 나눠 재계산하는가 | 하루치 기록의 결함 통계 작성 |
| [11. 스트림 처리](./%5B11%5D%20Stream%20Processing/README.md) | 계속 들어오는 기록을 어떻게 처리하는가 | 늦은 보고·중복 전송을 반영한 현황 갱신 |
| [12. 데이터 시스템의 방향](./%5B12%5D%20The%20Future%20of%20Data%20Systems/README.md) | 여러 도구를 정확하고 감사 가능하게 연결하는가 | 원본·현황·통계를 같은 이력에서 생성 |

<br>

### 반복해서 나오는 용어

| 용어 | 이 요약에서의 의미 |
| --- | --- |
| node | 계산·저장을 담당하는 process 또는 장비 |
| replica | 같은 논리 데이터의 복사본 |
| partition | 나눠 맡는 데이터의 부분 집합 |
| log | 순서대로 추가하는 변경·event 기록 |
| snapshot | 특정 기준 시점의 일관된 데이터 상태 |
| schema | field·type 등 데이터 구조의 약속 |
| invariant | 업무 전후에 유지돼야 하는 규칙 |
| idempotent | 같은 작업을 반복 적용해도 효과가 한 번과 같음 |
| system of record | 판단 기준이 되는 원본 저장소 |
| derived data | 원본을 가공해 만든 색인·집계 등 |

- 복제는 같은 것을 여러 곳에 두는 일, 분할은 서로 다른 부분을 나눠 맡는 일임
- 최신 정보가 늦게 보이는 문제와 기록이 누락·중복·손상된 문제를 구분해야 함
- 도구 이름보다 필요한 보장, 실패 조건, 복구 경로를 먼저 확인하는 것이 책 전체의 공통 관점임
