# Key

## 데이터 베이스 키(Key)의 개념

키(Key)는 DB에서 조건에 만족하는 튜플을 찾거나 순서대로 정렬할 때 다른 튜플들과 구별할 수 있는 유일한 기준이 되는 Attribute(속성)이다.

## Key의 종류

- 슈퍼 키(Super Key) : **`유일성`**을 만족하는 키.
(ex. 주민등록번호 + 이름 / 학번 + 이름 등…)
- 복합 키(Composite Key) : **`2개 이상의 속성`**(Attribute)를 사용한 키.
- 후보 키(Candidate Key) : `**유일성**`과  **`최소성`**을 만족하는 키. **`기본 키가 될 수 있는 후보`**이기 때문에 후보 키라고 불린다.
(ex. 주민등록번호, 학번 등…)
- **기본 키(Primary Key)** : 후보 키에서 선택된 키. **`NULL값이 들어갈 수 없으며`**, 기본키로 선택된 속성(Attribute)은 **`동일한 값이 들어갈 수 없다.`**
- 대체 키(AlternateKey) : 후보 키 중에 기본 키로 선택되지 않은 키.
- 외래 키(Foreign Key) : 어떤 테이블(Relation)간의 기본 키(Primary Key)를 **`참조하는 속성`**. 테이블(Relation)들 간의 관계를 나타내기 위해서 사용된다.
- 추가적인 키들 : 대리 키(Surrogate Key), 자연 키(Natural Key) 등…

![Untitled](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/c2078a16-aef3-4a0b-a6aa-52f96fc24ffc)


---

### 슈퍼 키(Super Key)

→ 어떤 속성끼리 묶던 중복 값이 안나오고 서로 구별만 할 수 있으면 된다. (유일성)

![Untitled 1](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/266fc09f-2045-4c88-86f0-152079a89fd0)


(ex. 학번 + 주민번호 + (이름 + 나이))

위 속성들을 가지고 하나의 유일한 값을 만들 수 있다면 이것을 슈퍼키라고 부를 수 있다.

---

### 후보 키(Candidate Key)

→ 슈퍼 키들 중에서 최소한의 속성의 갯수로 구별할 수 있는 키

![Untitled 2](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/13990d09-c50d-48e0-baf1-3fcdd62fadeb)


(ex. 학번, 주민번호)

(이름 + 나이)의 경우 유일성은 만족하지만, 학번과 주민번호처럼 유일성을 만족하는 속성의 갯수가 최소성(학번과 주민번호는 1개인데 비해, 이름 + 나이는 2개의 속성)을 만족하지 못하기 때문에 후보 키가 될 수 없다.

---

### 대체 키(Alternate Key)

→ 후보 키가 두 개 이상일 경우 그 중 어느 하나를 기본 키(Primary Key)로 지정하고, 남은 후보 키들을 대체 키(Alternate Key)라고 한다.

![Untitled 3](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/cc7de135-f97d-4959-a984-70a4684e7070)


(ex. 학번이 기본 키(Primary Key)로 선택된 경우)

후보 키인 주민번호는 대체 키가 된다.

---

### 외래 키(Foreign Key)

→ 다른 테이블을 참조할 때 가져오는 기본 키(Primary Key)를 외래키(Foreign Key)라고 한다.

![Untitled 4](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/5f860b9a-d18e-4538-af1b-d0fbd79bcb23)



(ex. 수강 테이블에서 학생 테이블을 참조하는 경우)

학생 테이블의 학번(기본 키)는 수강 테이블의 외래 키(Foreign Key)가 된다.

부모 테이블 : 학생 테이블 / 자식 테이블 : 수강 테이블

이 때, 테이블 삭제 순서는 수강 → 학생 순이다.
