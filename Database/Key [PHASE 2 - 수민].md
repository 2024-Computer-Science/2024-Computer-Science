## 키

- 투플을 **유일**하게 식별할 수 있는 애트리뷰트 집합

### 후보키(Candidate Key)

1. 유일성(uniqueness) : 각 투플은 유일해야함
2. 최소성(minimality) : 꼭 필요한 속성으로만 구성

위 두 속성을 만족하면 후보키가 된다.

### 슈퍼키 (Super Key)

- 유일성은 만족하지만 최소성이 만족되지 않는 애트리뷰트의 집합
- key를 포함하는 모든 속성의 집합

### 기본키 (primary key)

- 후보 키 중에서 데이터베이스 설계자가 지정한 하나의 키
- 각 투플에 대한 기본 키 값은 항상 유효(NULL일 수 없음)

### 대체키(alternate key)

- 후보 키 중에 기본 키를 제외한 나머지 후보 키

![image](https://github.com/user-attachments/assets/57095595-3fee-4504-9d32-6e76c256d59f)

### 외래키 (Foreign Key)

- 다른 릴레이션의 기본키를 그대로 참조하는 속성의 집합
