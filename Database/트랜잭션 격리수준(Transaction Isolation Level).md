# ⭐️트랜잭션 격리수준(Transaction Isolation Level)

### 여러 트랜잭션이 동시에 처리될 때, 특정 트랜잭션이 다른 트랜잭션에서 변경하거나 조회하는 데이터를 허용하도록 하는 수준

### 필요성

데이터베이스는 트랜잭션이 독립적으로 수행되게 하기 위해 Locking을 이용한다. 하나의 트랜잭션이 DB를 다루는 동안 다른 트랜잭션이 관여하지 못하도록 막는 것이다.

하지만 무조건 Locking으로 동시에 수행되는 많은 트랜잭션을 순서대로 처리하도록 하면 성능이 떨어진다. 그렇다고 해서 Locking의 범위를 줄이면, 잘못된 값을 처리할 수도 있는 문제가 발생한다.

→ 따라서 효율적인 격리수준을 사용해야한다.

<img width="834" alt="스크린샷 2024-05-01 오후 9 39 09" src="https://github.com/2024-Computer-Science/2024-Computer-Science/assets/83461362/85962c61-a1ea-435e-bd53-a4afb90c7389">

### Dirty Read

커밋 되지 않은 수정중인 데이터를 다른 트랜잭션에서 읽을 수 있도록 허용할 때 (Read Uncommitted) 발생하는 현상으로, **어떤 트랜잭션에서 아직 실행이 끝나지 않은 다른 트랜잭션에 의한 변경사항을 보게되는 경우**를 말한다.

### Non-Repeatable Read

- 한 트랜잭션 안에서 같은 쿼리를 두 번 실행 했을 때 다른 값이 나오는 READ 현상을 말한다. 하나의 트랜잭션에서 여러 스냅샷이 사용된다.
- 특정 데이터에 대한 **UPDATE**에 의해 나타나는 현상이다.

격리 수준이 Read Committed(level 1)일때를 살펴보자!

![image](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/83461362/874c7230-654a-4143-819c-50939a37004b)


만약 이 상황에서 T1이 update를 한 이후 T2가 읽는다면, 전에 읽었던 A와 같은 값이 나오게 된다.(Dirty Read는 일어나지 않음) 하지만 T1이 update 이후 Commit을 한 다음 T2에서 A를 읽으면 전에 읽었던 A값이 아닌 T1에서 update한 A값을 읽게 된다는 것이 문제이다.

**하나의 트랜잭션에서 똑같은 SELECT 쿼리를 실행했을 때는 항상 같은 결과를 가져와야 한다. 하지만 이 경우 일관성이 깨짐**

### Phantom Read

- 한 트랜잭션 안에서 첫번째 쿼리 수행 결과와 두번째 쿼리 수행 결과를 비교했을 때 첫번째 쿼리에서 없었던 레코드가 두번째 쿼리에서 나타나는 현상으로, 동시 실행중인 트랜잭션의 **INSERT**작업에 의해 발생하는 READ현상이다. 트랜잭션 도중 새로운 레코드 삽입을 허용하기 때문에 나타난다.

<img width="775" alt="스크린샷 2024-05-01 오후 9 39 46" src="https://github.com/2024-Computer-Science/2024-Computer-Science/assets/83461362/06194b99-46ba-45a4-8a97-f998e18f57db">

<img width="747" alt="스크린샷 2024-05-01 오후 9 40 35" src="https://github.com/2024-Computer-Science/2024-Computer-Science/assets/83461362/279f6554-057c-4d56-8ecd-bebe41b433fe">


이를 통해, MySQL의 Repeatable Read 격리 수준에서는 Phantom read현상이 대부분 일어나지 않는 것을 알 수 있다.

### 왜?

**MVCC(다중 버전 동시성 제어)** 를 이용하기 때문이다.


> 💁🏼‍♀️ InnoDB Storage Engine은 트랜잭션이 Rollback될 가능성에 대비해 변경되기 전 레코드를 Undo log에 백업해두고 실제 레코드 값을 변경한다.
트랜잭션이 COMMIT을 하기전에 다른 세션에서 해당 데이터를 조회할 때 UNDO를 참조하여 이전 값을 보여주는 것을 **MVCC**라고 한다.


> 💁🏼‍♀️ Repeatable read는 MVCC를 위해 **UNDO 에 백업된 이전 데이터를 이용**하여 **동일 트랜잭션 내에서 동일한 결과**를 계속 보여줄 수 있게 보장한다.


하지만 모든 읽기 작업에서 Phantom read현상이 일어나지 않는 건 아니다! `SELECT .. FOR UPDATE`같은 쿼리를 실행하면 Phantom Read가 발생한다. 언두 레코드에는 Lock을 걸 수 없기 때문에 현재 레코드의 값을 가져오기 때문이다. 따라서 Next-Key Lock과 같은 기법을 이용할 수 있다.

### Next-Key Lock

Gap Lock과 Record Lock을 결합한 Lock이다.

**Gap Lock** : 현재 읽는 범위와 다음 인덱스 레코드 사이에 적용해 다른 트랜잭션이 새로운 레코드를 삽입하는 것을 방지한다.

**Record Lock** : 각 인덱스 레코드에 설정되며 단일 레코드에 대한 읽기 및 쓰기 작업을 보호한다.

InnoDB 스토리지 엔진은 인덱스를 검색하거나 스캔할 때 공유 락 또는 배타 락을 걸게 된다. 이는 레코드 레벨의 잠금인데, Next-Key Lock 같은 경우는 인덱스 레코드에 대한 락 외에도 인덱스 레코드 이전의 Gap에 대해 락을 걸어 Phantom Read를 방지한다.

`SELECT * FROM child WHERE id > 100 FOR UPDATE;` 쿼리를 날렸을 때 100 보다 큰 첫 번째 레코드에 대해 락을 걸게 된다. 예를들어 101이 없고, 다음 ID가 102인 경우 101에 대한 INSERT를 막지 못하게 된다. 102 이상의 값에 대해서만 락이 걸려 데이터를 생성할 수 없게 기 때문이다.

즉 ID가 101인 경우 레코드를 Insert할 수 있는데, Next-Key Lock을 사용하게 되면 100 ~ 102 사이의 갭과 102 이상의 레코드에 락이 걸리기 때문에 101을 Insert할 수 없게 되어 Phantom Read를 방지할 수 있게 된다.
