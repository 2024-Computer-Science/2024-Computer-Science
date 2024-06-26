# ⭐️트랜잭션(Transaction)

### 데이터베이스 상태를 변화시키기 위해 수행하는 작업 단위

상태 변화 → SQL 질의어를 통해 DB에 접근하는것 (select ,insert, delete, update)

작업 → 많은 SQL 명령문들을 묶어 하나의 작업을 실행. 여러 쿼리문들이 모두 성공적으로 완료되어야만 하나의 트랜잭션(작업)이 완료된다.

- 여러 사용자가 동시에 동일한 데이터베이스 공유 가능하도록 지원⭐️
- 동시에 사용하더라도 **일관성(Consistency)** 를 ****보장하기 위한 동시성 제어

- 트랜잭션의 주요 성질: **ACID, jim gray**
    - **원자성(Atomicity)**: 트랜잭션과 관련된 작업들이 **부분적으로 실행되다가 중단되지 않는 것을 보장**하는 능력
    - **일관성(Consistency):** 트랜잭션이 실행을 성공적으로 완료하면 **언제나 일관성 있는 데이터베이스 상태로 유지**하는 것을 의미
    - **격리성(Isolation)**: 트랜잭션 수행 시 **다른 트랜잭션의 연산 작업이 끼어들지 못하도록 보장**하는 것을 의미
    - **영속성(Durability)**: 성공적으로 수행된 트랜잭션은 **영원히 반영**되어야 함
    

### 트랜잭션의 원자성을 위한 연산

- Commit(완료)
    - 트랜잭션의 성공적인 실행
        - 일관성 있는 데이터베이스 상태
    - 영구적인 갱신
    - 갱신된 데이터의 영속성을 보장
- Rollback(복귀)
    - 트랜잭션 실행의 실패. 하나의 트랜잭션 처리가 비정상적으로 종료되어 원자성이 깨진 경우
        - 모순된 데이터베이스 상태
    - 수행한 모든 연산 결과의 **UNDO**
    

### 프로세스 상태

![image](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/83461362/11511142-d3dc-43e1-8f4f-3f2e81e78832)

- 활동, 부분완료까지는 메모리에서 진행되고, commit이 되는 순간 disk에 저장된다.
- 트랜잭션 실패하여 rollback 후 철회할 때, 재시작의 권한은 DB에게 없다.
- 프로그램: 하나 이상의 트랜잭션을 포함
    - 모든 트랜잭션의 성공적인 완료 → 프로그램의 성공적인 수행

### 실패 상태에 있는 트랜잭션

- 데이터베이스 상태를 트랜잭션 실행이 시작되기 직전의 상태로 환원 시키기 위해 Rollback연산을 실행함.
- 그 뒤 철회 상태의 트랜잭션으로 되어 종료
- 이 때 트랜잭션의 재시작, 트랜잭션의 폐기 등의 조치를 취할 수 있다.
    - 재시작: 하드웨어나 시스템 소프트웨어 오류로 인해 철회된 트랜잭션은 다시 새로운 트랜잭션으로 취급되어 재시작
    - 폐기: 트랜잭션의 내부적 오류로 재작성을 해야 하거나 원하는 데이터가 데이터베이스에 없는 경우 취하는 조치

### Transaction 관리를 위한 DBMS의 전략



1. DBMS의 구조
- Query Processor (질의 처리기)
- Storage System (저장 시스템)

![image](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/83461362/11ab7228-697f-47c8-933b-3bab72b09e9c)

2. Page Buffer Manager or Buffer Manager

DBMS의 Storage System에 속하는 모듈 중 하나로, **Main Memory에 유지하는 페이지를 관리하는 모듈**이다.

Buffer 관리 정책에 따라, UNDO 복구와 REDO 복구가 요구되거나 그렇지 않게 되므로, Transaction 관리에 매우 중요한 결정을 가져온다.

3. UNDO

**정상적으로 종료되지 않은 Transaction이 변경한 page들은 원상 복구** 되어야 하는데, 이 복구를 undo라고 한다. 

**수정된 페이지를 디스크에 쓰는 시점을 기준으로 2개의 버퍼 교체 정책**

- **STEAL**: 수정된 페이지를 언제든지 디스크에 쓸 수 있는 정책
    - 대부분의 DBMS가 채택하는 Buffer 관리 정책
    - **UNDO logging과 복구**를 필요로 한다.
- ¬STEAL: 수정된 페이지들을 최소한 트랜잭션 종료 시점(EOT, End of Transaction)까지는 버퍼에 유지하는 정책

만약 버퍼 관리자가 트랜잭션 종료 전에는 어떤 경우에도 수정된 페이지를 디스크에 쓰지 않는다면, UNDO 오퍼레이션은 메모리버퍼에 대해서만 이루어지면 되는 식으로 간단해질 수 있지만, 매우 큰 크기의 메모리 버퍼가 필요하다는 문제점이 있다. 따라서 대부분의 DBMS는 **STEAL 정책을 쓰고, UNDO 로그**를 이용하여 모든 변경을 취소시킴으로써 원래 데이터베이스를 복원한다.

4. REDO

**이미 Commit한 Transaction의 수정을 재반영**하는 **복구 작업**을 REDO라고 한다. UNDO와 마찬가지로 Buffer 관리 정책에 영향을 받는다.

**Transaction이 종료되는 시점에 해당 Transaction이 수정한 page를 디스크에 쓸 것인가 아닌가로 2가지 정책**

- FORCE: 수정했던 모든 페이지를 트랜잭션 커밋 시점에 디스크에 반영하는 정책
    - Transaction이 Commit되었을 때 수정된 페이지들이 disk 상에 반영되므로 REDO가 필요 없다.
- **¬FORCE**: 수정했던 페이지를 트랜잭션 커밋 시점에 디스크에 반영하지 않는 정책
    - Transaction이 disk 상의 db에 반영되지 않을 수 있기에 REDO가 필요함.
    - 대부분의 DBMS 정책

가장 최근의 복제본을 적재시킨 뒤, 이 복제본 이후에 일어난 변경만을 **REDO 로그**를 이용하여 재실행함으로써 데이터베이스를 복원하는 방식을 사용하여 REDO한다.

### 정리

→DBMS는 버퍼 관리 정책으로 STEAL과 ¬FORCE를 채택하므로, UNDO 복구와 REDO 복구가 모두 필요하다.
