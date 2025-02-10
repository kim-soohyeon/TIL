# 데이터베이스의 유형과 활용

데이터베이스는 특징에 따라 **열 기반 데이터베이스(column-oriented database)**, **키-값 데이터베이스(key-value database)**, **문서 기반 데이터베이스(document-based database)** 등으로 분류됩니다.

## 관계형 데이터베이스(Relational Database)

관계형 데이터베이스는 데이터를 **표(Table) 형식**으로 관리하며, 데이터 간의 **관계(Relation)** 를 중시하는 데이터베이스입니다. 주로 **정형 데이터(Structured Data)** 를 다루며, **데이터 무결성(Integrity)과 일관성(Consistency)** 을 보장하는 것이 특징입니다. 또한, **SQL(Structured Query Language)** 을 사용하여 데이터를 쉽게 조회하고 조작할 수 있습니다.

그러나 관계형 데이터베이스는 **비정형 데이터(Unstructured Data)** 를 다루는 데 적합하지 않을 수 있습니다. 예를 들어, 대규모의 실시간 스트리밍 데이터나 이미지, 동영상 등의 데이터를 관계형 데이터베이스에 저장하면 **오버헤드(Overhead)** 가 발생할 수 있습니다. 이러한 경우에는 **NoSQL** 데이터베이스를 활용하는 것이 더 적합합니다.

### 행 지향 데이터베이스 (Row-Oriented Database)

- **OLTP(Online Transaction Processing)** 시스템에 적합
- 은행 거래, 온라인 쇼핑 등 **실시간 트랜잭션**이 많은 환경에서 사용
- 데이터를 행(Row) 단위로 저장하므로 **읽기/쓰기 성능이 균형적**
- 대표적인 DBMS: **MySQL, PostgreSQL, Oracle, MSSQL**

### 열 지향 데이터베이스 (Column-Oriented Database)

- **OLAP(Online Analytical Processing)** 시스템에 적합
- 데이터 분석, 빅데이터 처리와 같은 **읽기 연산이 많은 환경**에서 사용
- 특정 열(Column)만 메모리에 적재하여 처리하므로 **디스크 I/O를 줄이고 성능을 향상**
- 데이터의 일관성과 무결성을 보장하지만, **데이터 추가/수정이 빈번한 환경에서는 성능 저하 발생 가능**
- 대표적인 DBMS: **SAP HANA, Amazon Redshift, Google BigQuery**

## SSD(Solid State Drive)

최근에는 **SSD(Solid State Drive)** 가 기존의 **HDD(Hard Disk Drive)** 를 대체하며 데이터베이스 성능 개선에 기여하고 있습니다. 특히 **열 지향 데이터베이스**는 데이터를 **열 단위로 저장**하여 **I/O 작업을 최소화**할 수 있기 때문에, **SSD 환경에서 최적의 성능을 발휘**할 수 있습니다.
