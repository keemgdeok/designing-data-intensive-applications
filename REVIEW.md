## Designing Data-Intensive Applications

### 검토 범위

- 검토일: 2026-11-05
- 기준: Martin Kleppmann, 2017년 초판, 로컬 PDF 613쪽
- 대상: 12개 장 README, 루트 목차, 이 검토 기록
- 원문 목차·PDF 북마크의 절과 하위 절 181개를 반영함. 각 장의 Summary를 포함한 수임
- 목차에 없는 세부 논점은 해당 절의 하위 제목 또는 bullet로 정리함. 원문의 문단별 번역이나 참고문헌별 해설은 범위에 포함하지 않음
- 항공정비 예시는 개념 설명용으로 작성함. 책의 원래 사례와 구분함

<br>

### 원문 범위와 그림 대조

- PDF 쪽수는 file의 첫 페이지를 1로 센 값임. 인쇄 본문 쪽수와 22쪽 차이가 있음
- 장 시작은 실제 `CHAPTER` heading으로, 끝은 Summary와 References 시작으로 확인함
- 참고문헌이 요약과 같은 페이지에서 시작하는 경우 아래 요약 범위와 겹침
- 다음 장 시작도 확인함. 마지막 장 이후에는 Glossary가 시작됨

| 장 | 요약한 본문 쪽수 | PDF 쪽수 | References 시작 PDF | 목차 항목 | 그림 |
| --- | --- | --- | --- | --- | --- |
| 01 | 3–23 | 25–45 | 45 | 15 | 1-1~1-5, 5개 |
| 02 | 27–64 | 49–86 | 86 | 16 | 2-1~2-6, 6개 |
| 03 | 69–104 | 91–126 | 126 | 15 | 3-1~3-12, 12개 |
| 04 | 111–140 | 133–162 | 162 | 11 | 4-1~4-7, 7개 |
| 05 | 151–193 | 173–215 | 215 | 20 | 5-1~5-14, 14개 |
| 06 | 199–218 | 221–240 | 240 | 14 | 6-1~6-8, 8개 |
| 07 | 221–267 | 243–289 | 290 | 13 | 7-1~7-11, 11개 |
| 08 | 273–312 | 295–334 | 334 | 17 | 8-1~8-5, 5개 |
| 09 | 321–375 | 343–397 | 397 | 16 | 9-1~9-10, 10개 |
| 10 | 389–431 | 411–453 | 453 | 14 | 10-1~10-3, 3개 |
| 11 | 439–481 | 461–503 | 503 | 14 | 11-1~11-7, 7개 |
| 12 | 489–544 | 511–566 | 567 | 16 | 12-1, 1개 |

- 장 시작 PDF: 25, 49, 91, 133, 173, 221, 243, 295, 343, 411, 461, 511쪽. Glossary는 575쪽에서 시작함
- 원문의 번호가 붙은 figure 89개, 기존 PNG 89개, README image reference 89개가 대응함
- 각 그림을 원문 embedded image·caption과 대조하고, 89개 전체를 contact sheet로 열어 내용·순서를 확인함
- 기존 PNG 중 일부는 흑백 변환돼 있어 원문 추출본과 픽셀 값이 완전히 같지는 않음. 크기·내용·caption의 대응을 확인해 재사용함
- 신규·교체 이미지 0개. 모든 image tag에 번호와 설명을 포함한 `alt`를 추가함

<br>

### 내용 검토에서 보완한 구분

- fault와 서비스 failure, 원본 기록과 파생 현황을 구분함
- quorum의 교집합이 linearizability를 자동 보장한다는 해석을 피함
- transaction의 atomicity와 isolation, ACID consistency와 replica consistency를 구분함
- snapshot isolation과 serializability를 구분하고, SSI를 모든 오래된 읽기의 무조건 취소로 설명하지 않도록 수정함
- 2PL은 격리, 2PC는 commit 조정이라는 차이를 표시함
- timeout을 작업 미수행의 증명으로 해석하지 않도록 설명함
- fencing token은 resource가 검사해야 효과가 있다는 조건을 유지함
- Lamport 정렬과 확정된 실행 순서, partition 순서와 전역 순서를 구분함
- stream-table join은 최신 정보와 당시 version 중 어떤 의미를 원하는지 명시하도록 설명함
- exactly-once는 내부 실행 횟수보다 관측되는 효과의 보장 범위로 설명함
- 원자적 commit이 최신 읽기·직렬성을 자동 제공하지 않는다는 조건을 명시함
- 12장의 비동기 제약 검사와 보정은 저자의 설계 제안으로 다룸. 모든 업무의 즉시 보장을 대체하는 방식으로 일반화하지 않음

<br>

### 공식 문서 대조

- 2장: [MongoDB Map-Reduce](https://www.mongodb.com/docs/manual/core/map-reduce/) — 책의 예시와 MongoDB 5.0부터의 deprecation 안내를 분리함
- 4장: [Python pickle](https://docs.python.org/3/library/pickle.html) — 신뢰할 수 없는 데이터의 역직렬화 위험을 확인함
- 4장: [Protocol Buffers proto3](https://protobuf.dev/programming-guides/proto3/) — field 번호 재사용과 reserved, field presence의 버전·문법 맥락을 확인함
- 4장: [Avro 1.12.0 Schema Resolution](https://avro.apache.org/docs/1.12.0/specification/#schema-resolution) — writer·reader schema, 누락 field와 default의 조건을 확인함
- 7장: [PostgreSQL Transaction Isolation](https://www.postgresql.org/docs/current/transaction-iso.html) — repeatable read와 serializable의 차이, 전체 transaction 재시도 조건을 확인함
- 9장: [etcd 3.6 API guarantees](https://etcd.io/docs/v3.6/learning/api_guarantees/) — 기본 linearizable read와 serializable read의 차이를 확인함
- 11장: [Kafka 4.1 Message Delivery Semantics](https://kafka.apache.org/41/design/design/#message-delivery-semantics) — topic 간 처리와 외부 저장소 출력의 보장 범위를 구분함

<br>

### 로컬 검증

- `git diff --check`: tracked 변경의 공백 오류 없음
- 새 루트 README와 REVIEW는 각각 `git diff --no-index --check /dev/null <file>`로 별도 확인함
- 원문 목차 항목 181개의 제목·계층을 장 README와 대조함. 누락 없음
- heading 단계, 표 column 수, code fence, 내부 링크·image 경로, `alt`, 그림 번호·개수를 확인함
- 루트와 12개 장을 375px·1280px의 로컬 Markdown HTML로 렌더링함
- 표와 그림이 많은 3·7장, 루트 목차는 두 폭의 화면을 직접 확인함. 3장 비교 표의 과도한 줄바꿈을 줄임
- 위 렌더링은 로컬 미리보기 기준임. 작은 화면의 세밀한 원문 도해는 확대해서 읽어야 함
- 검증용 추출물·HTML·화면 이미지는 repository 밖의 임시 경로에만 생성함

<br>

### Git 범위

- 수정: 기존 장 README 12개
- 추가: 루트 `README.md`, `REVIEW.md`
- 기존 untracked `AGENTS.md`와 원본 PDF는 수정·stage하지 않음
- 이미지 binary 변경 없음. 임시 파일·generator·자동화 추가 없음
- commit·push 수행하지 않음

<br>

### 그림 배치와 세부 주제 보완

- 3장: 값의 저장 위치·복합 색인·전문 및 유사 검색·memory 저장을 원문 하위 제목으로 구분함. B-tree의 복구와 최적화도 분리함
- 4장: BinaryProtocol·CompactProtocol·Protocol Buffers의 차이를 각 그림 바로 앞에 설명함. field 번호·type 변경·Avro의 schema 해석과 전달을 나눔
- 12장: 전역 순서·인과관계·view 재처리·lambda architecture·상태 분리·다중 partition 처리·감사 가능성 등을 원문 하위 제목으로 구분함
- 2·5·7·9장: 연속된 그림의 설명을 각 그림 앞에 배치함. 7장은 SSI의 두 감지 대상과 성능 논점을 구분함
- 수정한 장은 2·3·4·5·7·9·12장임. 나머지 장은 같은 배치 문제가 있는지 확인한 뒤 유지함
- 검토한 그림들은 서로 다른 표현·단계·조건을 설명하므로 89개를 유지함. 추가·삭제·교체한 이미지 binary 없음
- 추가한 하위 제목을 원문 본문과 대조함. 목차 항목 181개의 제목과 계층, 기존 주장·조건·예외의 유지 여부를 다시 확인함
- heading·표·내부 링크·그림 경로·번호·설명 순서와 공백 오류를 재검사함
- 수정 후 375px·1280px로 재렌더링하고, 3·4·7·12장의 보완 구간을 두 폭에서 직접 확인함
