# Transaction

# 1. 트랜잭션(Transaction)이란?

→ 데이터 베이스의 상태를 변경시키는 작업의 단위. 즉, 한꺼번에 수행되어야 할 연산을 모아놓은 것.

ex) 은행에서 돈을 출금하는데, 돈을 출금하는 과정과 전산상에서 데이터가 갱신되는 과정이 한 묶음의 단위로 일어나야 함. 그렇지 않으면 돈은 출금했음에도 불구하고, 데이터가 갱신이 안되서 잘못 계산되는 일이 발생.

![image](https://github.com/user-attachments/assets/8edf7262-80d6-4f24-9426-169ebca20136)


# 2. 트랜잭션의 네 가지 특징(ACID)

## 1. 원자성(Atomicity)

트랜잭션이 DB에 모두 반영되거나, 혹은 전혀 반영되지 않아야 한다.

## 2. 일관성(Consistenty)

트랜잭션의 작업 처리 결과는 항상 일관성 있어야 한다.

즉, 시스템이 가지고 있는 고정 요소는 트랜잭션 수행 전과 수행 후의 상태가 같아야 한다는 말.

ex) 송금 시 금액의 데이터 타입을 정수형(Integer)에서 문자열(String)로 변경할 수 없다.

## 3. 독립성(Isolation)

둘 이상의 트랜잭션이 동시에 병행 실행되고 있을 때, 어떤 트랜잭션도 다른 트랜잭션 연산에 끼어들 수 없다.

## 4. 지속성(Durability)

트랜잭션이 성공적으로 완료되었으면, 결과는 영구적으로 반영되어야 한다.

~~→ Spring의 @Transactional 어노테이션이 save()를 사용하지 않아도 디비에 반영되는 것도 같은 원리?.~~.

# 3. 트랜잭션의 연산

## 1) Commit 연산

트랜잭션이 성공적으로 수행되었음을 선언하는 연산. 최종 결과를 DB에 반영

## 2) Rollback 연산

트랜잭션 수행이 실패했음을 선언하고 현재까지의 작업을 모두 취소하는 연산. 트랜잭션 수행 전 상태로 되돌린다.

# 4. 트랜잭션의 상태

![image 1](https://github.com/user-attachments/assets/29c5264a-df6b-472d-841f-14fe64a5facf)

![image 2](https://github.com/user-attachments/assets/cf1d574c-feaa-4097-853b-3f1901aa0c56)

## Active

트랜잭션 활동 상태, 트랜잭션이 실행 중이며 동작 중인 상태

## Partically Committed

트랜잭션의 Commit 명령이 도착한 상태 → Committed는 완료된 상태, Partically Committed는 도착만 한 상태

트랜잭션의 SQL문이 수행되고, Commit을 수행하기 직전 상태

## Failed

트랜잭션 실패 상태

더이상 트랜잭션이 정상적으로 진행될 수 없는 상태

## Committed

트랜잭션 완료 상태

트랜잭션이 정상적으로 완료된 상태

## Aborted

트랜잭션 취소 상태

트랜잭션이 취소되고, 트랜잭션 실행 이전 데이터로 돌아간 상태(Rollback 연산을 실행한 상태)

---

# Transaction 관리를 위한 DMBS의 전략

1. 

---

https://velog.io/@shasha/Database-트랜잭션-정리
