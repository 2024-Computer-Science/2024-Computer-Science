# Join

## 조인

→ 복수의 테이블을 결합하는 것으로, 데이터 조회 시 다른 테이블의 데이터를 함께 조회해야할 때 사용.

(복수의 테이블을 연결하려면, 적어도 하나의 칼럼을 서로 공유하고 있어야 한다.)

## Join의 종류

- INNER JOIN
- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- FULL OUTER JOIN
- CROSS JOIN
- SELF JOIN

---

### INNER JOIN

보통 JOIN이라고 얘기하면 INNTER JOIN을 지칭한다.

![Untitled](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/fc4602f9-05f1-4d98-9979-0934fd15df77)

![Untitled 1](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/b969bba3-726f-444a-9400-4d9e76549661)


(ex. 상품 코드를 공통 컬럼으로 가지고 있는 두 테이블을 JOIN하는 예시)

→ 두 테이블을 JOIN하고, 그 중 상품코드가 1인 데이터를 가져오는 예시

```jsx
SELECT A.상품코드 상품코드, A.상품명 상품명, B.재고수량 재고수량 // 조회할 컬럼
		FROM TableA as A // 결합할 테이블 명. as 이후는 별칭
				INNER JOIN TableB as B // 결합할 테이블 명. as 이후는 별칭
				ON A.상품코드 = B.상품코드 // 결합 조건
		WHERE A.상품코드 = 1 // WHERE절을 이용하여 특정 데이터만 골라낼 수도 있다.
```

<aside>
💡 JOIN에 대한 조건 → ON
데이터 필터링에 대한 조건 → WHERE

</aside>

---

### OUTER JOIN

공통 데이터 외에 어느 한 테이블에만 존재하는 데이터도 함께 결합하여 조회하는 방식

(어떤 테이블을 먼저 접근하냐에 따라 쿼리 성능에 영향을 미친다. → 드라이빙 테이블(접근하는 테이블)은 더 적은 데이터를 추출하는 테이블로 설정하는 것이 좋다)

![Untitled 2](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/25d89eeb-7b99-4bcb-b6e8-3d0ce00e7f8e)


OUTER JOIN에는 LEFT, RIGHT, FULL OUTER JOIN이 있다.

### LEFT OUTER JOIN

왼쪽 테이블을 기준으로 조인하는 방식

왼쪽 테이블의 모든 데이터와 오른쪽 테이블의 중복 데이터가 결합되었다.

![Untitled 1](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/ef955ce5-da22-4467-b0b1-a3ca288e16b4)


![Untitled 3](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/68716f0b-a826-4083-89a8-c15180296d53)


(ex. A 테이블을 기준으로 조인하는 예제)

```jsx
SELECT A.상품코드 상품코드, A.상품명 상품명, B.재고수량 재고수량
		FROM TableA as A
		LEFT JOIN TableB as B
		ON A.상품코드 = B.상품코드
```

이 때, 값이 없는 데이터는 null로 표시된다.

### RIGHT OUTER JOIN

오른쪽 테이블을 기준으로 조인하는 방식

오른쪽 테이블의 모든 데이터와 왼쪽 테이블의 중복 데이터가 결합되었다.

![Untitled 1](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/716a1efe-8752-44e1-8f04-e0a7d203f0aa)


![Untitled 4](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/36eb698a-7fec-48e8-a373-ddcaedc5ada9)


(ex. B 테이블을 기준으로 조인하는 예제)

```jsx
SELECT A.상품코드 상품코드, A.상품명 상품명, B.재고수량 재고수량
		FROM TableA as A
				RIGHT JOIN TableB as B
				ON A.상품코드 = B.상품코드
```

LEFT OUTER JOIN과 마찬가지로 값이 없는 데이터는 null로 표시된다.

### FULL OUTER JOIN

LEFT JOIN 결과와 RIGHT JOIN결과를 합친 결과를 얻을 수 있다.

![Untitled 3](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/d8c341ac-df1a-47fd-85d6-7066b1f857c6)


![Untitled 4](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/9630d417-536f-46f2-9494-e3f739e8099a)


![Untitled 5](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/565e6200-512e-4b86-967a-804f8fb73aa7)


```jsx
SELECT A.상품코드 상품코드, A.상품명 상품명, B.재고수량 재고수량
		FROM TableA as A
				FULL JOIN TableB as B
				ON A.상품코드 = B.상품코드
```

일반적으로 INNER JOIN을 많이 사용하며, OUTER JOIN중에서는 LEFT JOIN을 많이 사용한다.

---

### CROSS JOIN

모든 경우의 수를 전부 표현하여 결합하는 방식(카테시안 곱)

![Untitled 6](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/a3923910-4845-4188-aeda-c7889a94f1d5)


(ex. A 테이블과 B 테이블의 모든 결합 경우의 수를 표현해주는 예제)

```jsx
SELECT A.NAME, B.AGE
		FROM EX_TABLE A
				CROSS JOIN JOIN_TABLE B
```

---

### SELF JOIN

자기 자신을 JOIN하여 결합하는 방식

![Untitled 7](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/2eafd9a0-94c3-4911-94e5-6c4d173cfb77)


(ex. A테이블이 자기 자신을 JOIN하는 예제)

```jsx
SELECT A.NAME, B.AGE
		FROM EX_TABLE A, EX_TABLE B
```
