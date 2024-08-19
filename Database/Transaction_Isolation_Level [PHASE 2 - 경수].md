# Transaction Isolation Level

# 트랜잭션 격리 수준(Transaction Isoloation Level)

→ 여러 트랜잭션이 동시에 처리될 대, 특정 트랜잭션이 다른 트랜잭션에서 변경하거니 조회하는 데이터를 볼 수 있게 허용할지 여부를 결정하는 것

## Isolation Level의 필요성

- 트랜잭션이 DB를 다루는 동안 다른 트랜잭션이 관여하지 못하도록 막아야 하는데, 무조건 Locking을 통해 이 과정을 막게되면 DB의 성능은 떨어질 수 밖에 없다. 따라서 Isolation Level을 나눠 효율적으로 Locking을 하여 DB의 성능을 올려야 한다.

## 트랜잭션 격리 수준 종류

- SERIALIZABLE
- REPEATABLE READ
- READ COMMITTED
- READ UNCOMMITED

→ 격리 수준이 높은 순서대로이며, 모두 자동 커밋(Auto Commit)이 false인 상태에서 발생한다.

### 1. SERIALIZABLE [Level 3]

- 가장 엄격한 격리 수준
- 트랜잭션을 순차적으로 진행 → 동시 처리 성능 매우 낮음
- 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 공유락(Shared Lock)이 걸리는 계층
- 가장 안전하지만 가장 성능이 떨어지므로, 극단적으로 안전이 요구되는 작업이 아닌 이상 사용해서는 안됨.

### 2. REPEATABLE READ [Level 2]

- 트랜잭션이 시작되기 전에 커밋된 내용에 대해서만 조회할 수 있는 격리 수준
- 자신의 트랜잭션 번호보다 낮은 트랜잭션 번호에서 변경(혹은 커밋)된 것만 조회 가능
(모든 Inno DB의 트랜잭션은 순차적으로 증가하는 트랜잭션 번호를 가지고 있기에 가능)
- Phantom Read(유령 읽기) 문제가 발생
- 트랜잭션이 시작된 시점의 데이터를 일관되게 보여주는 것을 보장해야 하기 때문에, 한 트랜잭션의 실행 시간이 길어질수록 해당 시간만큼 계속 멀티 버전을 관리해야 하는 단점이 존재

<aside>
💡 Phantom Read (유령 읽기)
동일한 트랜잭션 내에서도 새로운 레코드가 추가되는 경우 조회 결과가 달라지는 현상이 발생하는데, 이처럼 다른 트랜잭션에서 수행한 작업에 의해 레코드가 보였다 안보였다 하는 현상을 말한다.

</aside>

### 3. READ COMMITTED [Level 1]

- 어떤 트랜잭션의 변경 내용이 COMMIT 되어야만 다른 트랜잭션에서 조회할 수 있는 격리 수준
- 온라인 서비스에서 가장 많이 선택됨
- Phantom Read 문제와 더불어 Non-Repeatable Read(반복 읽기 불가능) 문제까지 발생

<aside>
💡 Non-Repeatable Read (반복 읽기 불가능)
다른 트랜 잭션의 커밋 여부에 따라 조회 결과가 달라질 수 있는 데이터 부정합 문제

</aside>

### 4. READ UNCOMMITTED [Level 0]

- 커밋하지 않은 데이터 조차도 접근할 수 있는 격리 수준
- 다른 트랜잭션의 작업이 커밋 또는 롤백되지 않아도 즉시 보이기 때문에 Dirty Read(오손 읽기) 문제가 발생
- REMBS 표준에서 인정하지 않을 정도로 정합성에 문제가 많은 격리 수준
- 따라서 최소한 READ COMMITTED 격리 수준은 사용해야 한다.

<aside>
💡 Dirty Read (오손 읽기)
데이터가 조회되었다가 사라지는 문제

</aside>

---

# 트랜잭션 격리 수준 요약

<img width="927" alt="image" src="https://github.com/user-attachments/assets/9fed8e83-ea08-454d-bbb4-218c042f351a">


---

https://mangkyu.tistory.com/299

https://joont92.github.io/db/트랜잭션-격리-수준-isolation-level/
