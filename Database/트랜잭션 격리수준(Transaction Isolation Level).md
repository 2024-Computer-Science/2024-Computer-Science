# 트랜잭션 격리수준(Transaction Isolation Level)

### 여러 트랜잭션이 동시에 처리될 때, 특정 트랜잭션이 다른 트랜잭션에서 변경하거나 조회하는 데이터를 허용하도록 하는 수준

### 필요성

데이터베이스는 트랜잭션이 독립적으로 수행되게 하기 위해 Locking을 이용한다. 하나의 트랜잭션이 DB를 다루는 동안 다른 트랜잭션이 관여하지 못하도록 막는 것이다.

하지만 무조건 Locking으로 동시에 수행되는 많은 트랜잭션을 순서대로 처리하도록 하면 성능이 떨어진다. 그렇다고 해서 Locking의 범위를 줄이면, 잘못된 값을 처리할 수도 있는 문제가 발생한다.

→ 따라서 효율적인 격리수준을 사용해야한다.

| LEVEL 0 | READ UNCOMMITTED | 각 트랜잭션에서 변경내용이 Commit이나 Rollback여부에 상관 없이 다른 트랜잭션에서 값을 읽을 수 있다. | 데이터베이스 일관성을 유지할 수 없음.
Dirty Read 현상이 발생할 수 있음. |
| --- | --- | --- | --- |
| LEVEL 1 | READ COMMITTED | 어떠한 트랜잭션에서 데이터를 변경하더라도 COMMIT이 완료된 데이터만 다른 트랜잭션에서 조회가 가능하다. | 대부분의 SQL 서버가 Defualt로 사용. 하지만 non-repeatable Read라는 부정합 문제 발생 |
| LEVEL 2 | REPEATABLE READ | UNDO 영역에 백업된 이전 데이터를 통해 동일한 트랜잭션 내에는 동일한 결과를 보여주도록 한다. | 다른 사용자는 트랜잭션 영역에 해당되는 데이터에 대한 수정이 불가능. 입력은 가능. MySQL에서 Default로 사용. Phantom read 현상이 발생할 수 있음. |
| LEVEL 3 | SERIALIZABLE | 한 트랜잭션에서 읽고 쓰는 레코드를 다른 트랜잭션에서는 절대 접근할 수 없다. | 다른 사용자는 트랜잭션 영역에 해당되는 데이터에 대한 수정 및 입력이 불가능. 완벽한 읽기 일관성 모드
동시성이 중요한 DB에서는 거의 사용하지 않는다. |

### Dirty Read

커밋 되지 않은 수정중인 데이터를 다른 트랜잭션에서 읽을 수 있도록 허용할 때 (Read Uncommitted) 발생하는 현상으로, **어떤 트랜잭션에서 아직 실행이 끝나지 않은 다른 트랜잭션에 의한 변경사항을 보게되는 경우**를 말한다.

### Non-Repeatable Read

- 한 트랜잭션 안에서 같은 쿼리를 두 번 실행 했을 때 다른 값이 나오는 READ 현상을 말한다. 하나의 트랜잭션에서 여러 스냅샷이 사용된다.
- 특정 데이터에 대한 **UPDATE**에 의해 나타나는 현상이다.

격리 수준이 Read Committed(level 1)일때를 살펴보자!

![Untitled](%E1%84%90%E1%85%B3%E1%84%85%E1%85%A2%E1%86%AB%E1%84%8C%E1%85%A2%E1%86%A8%E1%84%89%E1%85%A7%E1%86%AB%20%E1%84%80%E1%85%A7%E1%86%A8%E1%84%85%E1%85%B5%E1%84%89%E1%85%AE%E1%84%8C%E1%85%AE%E1%86%AB(Transaction%20Isolation%20Level%204a4d636a204443cab1e734c3a7612a26/Untitled.png)

만약 이 상황에서 T1이 update를 한 이후 T2가 읽는다면, 전에 읽었던 A와 같은 값이 나오게 된다.(Dirty Read는 일어나지 않음) 하지만 T1이 update 이후 Commit을 한 다음 T2에서 A를 읽으면 전에 읽었던 A값이 아닌 T1에서 update한 A값을 읽게 된다는 것이 문제이다.

**하나의 트랜잭션에서 똑같은 SELECT 쿼리를 실행했을 때는 항상 같은 결과를 가져와야 한다. 하지만 이 경우 일관성이 깨짐**

### Phantom Read

- 한 트랜잭션 안에서 첫번째 쿼리 수행 결과와 두번째 쿼리 수행 결과를 비교했을 때 첫번째 쿼리에서 없었던 레코드가 두번째 쿼리에서 나타나는 현상으로, 동시 실행중인 트랜잭션의 **INSERT**작업에 의해 발생하는 READ현상이다. 트랜잭션 도중 새로운 레코드 삽입을 허용하기 때문에 나타난다.

Read committed 수준일 때를 보자.

![Untitled](%E1%84%90%E1%85%B3%E1%84%85%E1%85%A2%E1%86%AB%E1%84%8C%E1%85%A2%E1%86%A8%E1%84%89%E1%85%A7%E1%86%AB%20%E1%84%80%E1%85%A7%E1%86%A8%E1%84%85%E1%85%B5%E1%84%89%E1%85%AE%E1%84%8C%E1%85%AE%E1%86%AB(Transaction%20Isolation%20Level%204a4d636a204443cab1e734c3a7612a26/Untitled%201.png)

![Untitled](%E1%84%90%E1%85%B3%E1%84%85%E1%85%A2%E1%86%AB%E1%84%8C%E1%85%A2%E1%86%A8%E1%84%89%E1%85%A7%E1%86%AB%20%E1%84%80%E1%85%A7%E1%86%A8%E1%84%85%E1%85%B5%E1%84%89%E1%85%AE%E1%84%8C%E1%85%AE%E1%86%AB(Transaction%20Isolation%20Level%204a4d636a204443cab1e734c3a7612a26/Untitled%202.png)

- 첫번째 트랜잭션에서 insert하고, 두번째 트랜잭션에서 select로 확인했을 때 insert되지 않는다.

![Untitled](%E1%84%90%E1%85%B3%E1%84%85%E1%85%A2%E1%86%AB%E1%84%8C%E1%85%A2%E1%86%A8%E1%84%89%E1%85%A7%E1%86%AB%20%E1%84%80%E1%85%A7%E1%86%A8%E1%84%85%E1%85%B5%E1%84%89%E1%85%AE%E1%84%8C%E1%85%AE%E1%86%AB(Transaction%20Isolation%20Level%204a4d636a204443cab1e734c3a7612a26/Untitled%203.png)

![Untitled](%E1%84%90%E1%85%B3%E1%84%85%E1%85%A2%E1%86%AB%E1%84%8C%E1%85%A2%E1%86%A8%E1%84%89%E1%85%A7%E1%86%AB%20%E1%84%80%E1%85%A7%E1%86%A8%E1%84%85%E1%85%B5%E1%84%89%E1%85%AE%E1%84%8C%E1%85%AE%E1%86%AB(Transaction%20Isolation%20Level%204a4d636a204443cab1e734c3a7612a26/Untitled%204.png)

- commit후에 다시 select로 확인해보면 **insert가 되어있다.**

![Untitled](%E1%84%90%E1%85%B3%E1%84%85%E1%85%A2%E1%86%AB%E1%84%8C%E1%85%A2%E1%86%A8%E1%84%89%E1%85%A7%E1%86%AB%20%E1%84%80%E1%85%A7%E1%86%A8%E1%84%85%E1%85%B5%E1%84%89%E1%85%AE%E1%84%8C%E1%85%AE%E1%86%AB(Transaction%20Isolation%20Level%204a4d636a204443cab1e734c3a7612a26/Untitled%205.png)

**REPEATABLE READ**로 바꾸어서 실행해본다.

![Untitled](%E1%84%90%E1%85%B3%E1%84%85%E1%85%A2%E1%86%AB%E1%84%8C%E1%85%A2%E1%86%A8%E1%84%89%E1%85%A7%E1%86%AB%20%E1%84%80%E1%85%A7%E1%86%A8%E1%84%85%E1%85%B5%E1%84%89%E1%85%AE%E1%84%8C%E1%85%AE%E1%86%AB(Transaction%20Isolation%20Level%204a4d636a204443cab1e734c3a7612a26/Untitled%206.png)

- 첫번째 트랜잭션의 insert 이후에 두번째 트랜잭션에서 select를 해봐도 insert 되지않는다.

![Untitled](%E1%84%90%E1%85%B3%E1%84%85%E1%85%A2%E1%86%AB%E1%84%8C%E1%85%A2%E1%86%A8%E1%84%89%E1%85%A7%E1%86%AB%20%E1%84%80%E1%85%A7%E1%86%A8%E1%84%85%E1%85%B5%E1%84%89%E1%85%AE%E1%84%8C%E1%85%AE%E1%86%AB(Transaction%20Isolation%20Level%204a4d636a204443cab1e734c3a7612a26/Untitled%207.png)

- 첫번째 트랜잭션의 **commit 이후에도** 두번째 트랜잭션에서 select를 해봐도 insert되지 않는다.  (phantom read 현상이 발생하지 않는다.)
- 두번째 트랜잭션의 commit이후에야 select를 진행하면 insert된 것이 보인다.

이를 통해, MySQL의 Repeatable Read 격리 수준에서는 Phantom read현상이 대부분 일어나지 않는 것을 알 수 있다.

### 왜?

**MVCC(다중 버전 동시성 제어)**를 이용하기 때문이다.

<aside>
💁🏼‍♀️ InnoDB Storage Engine은 트랜잭션이 Rollback될 가능성에 대비해 변경되기 전 레코드를 Undo log에 백업해두고 실제 레코드 값을 변경한다.
트랜잭션이 COMMIT을 하기전에 다른 세션에서 해당 데이터를 조회할 때 UNDO를 참조하여 이전 값을 보여주는 것을 **MVCC**라고 한다.

</aside>

<aside>
💁🏼‍♀️ Repeatable read는 MVCC를 위해 **UNDO 에 백업된 이전 데이터를 이용**하여 **동일 트랜잭션 내에서 동일한 결과**를 계속 보여줄 수 있게 보장한다.

</aside>

하지만 모든 읽기 작업에서 Phantom read현상이 일어나지 않는 건 아니다! `SELECT .. FOR UPDATE`같은 쿼리를 실행하면 Phantom Read가 발생한다. 언두 레코드에는 Lock을 걸 수 없기 때문에 현재 레코드의 값을 가져오기 때문이다. 따라서 Next-Key Lock과 같은 기법을 이용할 수 있다.

### Next-Key Lock

`SELECT * FROM child WHERE id > 100 FOR UPDATE;` 쿼리를 날렸을 때 100 보다 큰 첫 번째 레코드에 대해 락을 걸게 된다. 예를들어 101이 없고, 다음 ID가 102인 경우 101에 대한 INSERT를 막지 못하게 된다.

이를 방지하기 위해 Next-Key Lock을 사용한다. Next-Key Lock은 Gap Lock과 Record Lock을 결합한 형태로 동작한다.

**Gap Lock** : 현재 읽는 범위와 다음 인덱스 레코드 사이에 적용해 다른 트랜잭션이 새로운 레코드를 삽입하는 것을 방지한다.

**Record Lock** : 각 인덱스 레코드에 설정되며 단일 레코드에 대한 읽기 및 쓰기 작업을 보호한다.

InnoDB 스토리지 엔진은 인덱스를 검색하거나 스캔할 때 공유락 또는 배타 락을 걸게 된다. 이는 레코드 레벨의 잠근인데, Next-Key Lock 같은 경우는 인덱스 레코드에 대한 락 외에도 인덱스 레코드 이전의 Gap에 대해 락을 걸어 Phantom Read를 방지한다.

예시를 들자면 ID가 100 102인 레코드가 있는 테이블에서 Next-Key Lock없이 트랜잭션이 실행되면 102 이상의 값에 대해서만 락이 걸려 데이터를 생성할 수 없다. 즉 ID가 101인 경우 레코드를 생성할 수 있는데, Next-Key Lock을 사용하게 되면 100~102 사이의 갭과 102 이상의 레코드에 락이 걸리기 때문에 Phantom Read에 대해 자유롭다.