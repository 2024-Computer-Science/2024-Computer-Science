## 내부조인 (Inner Join)

### 동등조인(equi join)

- dnumber=dno인 모든 투플을 선택해라

```sql
select * from employee join department on employee.dno = department=dno;
```

![image](https://github.com/user-attachments/assets/0c544447-babd-4731-888e-f0a06bb95b3c)

### 자연조인(natural join)

```sql
select * from employee join department;
```

- 동일한 타입과 이름을 가진 컬럼을 조인 조건으로 이용하는, 조인을 간단히 표현하는 방법.
- 조인 조건이 필요 없음!
- 반드시 두 테이블 간의 동일한 이름, 타입을 가진 컬럼이 필요함
- 조인에 이용되는 컬럼은 명시하지 않아도 자동으로 조인에 사용됨
- 동일한 이름을 갖는 컬럼이 있지만 데이터 타입이 다르면 에러 발생
    - t1의 id는 int이고, t2의 id는 varchar일 경우 에러 발생.


## 외부조인(outer join)

### Left Outer join

- 결과에 왼쪽 테이블의 모든 투플이 나옴
- 만약 오른쪽 테이블에 매칭되는 투플이 없으면 NULL로 채움

```sql
select * from employee e left join department d 
	on d.dno = e.dno;
```

employee의 부서가 아직 없어서 null일 경우 null로 채워져서 출력이 된다.

![image](https://github.com/user-attachments/assets/347a3677-c670-41bb-ba03-b140fee9f67f)

### Right Outer join

- 결과에 오른쪽 테이블의 모든 투플이 나옴
- 만약, 왼쪽 테이블에 매칭되는 투플이 없으면 NULL로 채움

```sql
select * from employee e right join department d 
	on d.dno = e.dno;
```

이번엔 department의 모든 튜플이나오고, 부서번호에 해당하는 employee가 없을 경우 null로 출력

![image](https://github.com/user-attachments/assets/cf60d960-95e6-48a4-9053-9aa9a0e30675)

### Full join

두 테이블의 모든 행이 포함되고, 조인조건에 일치하지 않으면 NULL로 표시

```sql
SELECT * 
FROM employee e
FULL JOIN department d
ON e.dno = d.dno;
```

![image](https://github.com/user-attachments/assets/13c06b4b-bf76-4b5c-b86f-527bf314868c)

### **Cartacian product (곱집합)**

가능한 모든 조합을 생성한다.

```sql
select * from employee,department;
```

![image](https://github.com/user-attachments/assets/8b42488e-c7a0-4a84-b5f8-dbd0f60da814)

---


## JOIN 구현 방식

### Nested loop Join

단순히 중첩 루프로 구현한다.

```sql
for (driving_table: driving_tables) {
	for (driven_table: driven_tables) {
    	if(is_match(driving_table, driven_table) join(driving_table, driven_table)
    }
}
```

두 테이블의 크기가 작을 경우 효과적이다. 

시간복잡도: O(R * S) 

R: 테이블 1의 row 수, S: 테이블 2의 row수

### sort merge Join

매칭되는 테이블이 어느 범위까지만 존재한다는 것을 확인해서 효율적으로 검사하는 방법.

정렬해서 탐색하므로써 중간에 더이상 원하는 테이블이 없음을 확인하고 탈출할 수 있다.

시간복잡도 : 정렬하는데 `O(|R|log|R| + |S|log|S|)`가 소모,

 정렬 후 탐색하는데 `O(|R|+|S|)`가 소모

nested loop에 비해서는 빠르지만, join 하는 테이블이 작은 경우 정렬 비용이 클 수 있다.

R이 1이고 S가 큰 경우 정렬 비용이 큼(이럴경우 정렬안하고 바로 탐색하는게 더 이득)

### Hash Join

해시 테이블에 데이터들을 등록해놔 매칭 여부를 판단한다.

동등 연산이 가능한 경우에만 사용할 수 있다.

시간복잡도 : O(R+S)로 가장 적게 소모된다.

단점: 해시 충돌, 해시 테이블 만드는 비용이 클 수 있음, 동등 연산이 가능한 경우에만 사용가능, 인덱스 사용 불가

💡인덱스
>NL Join과 sort merge Join은 인덱스를 사용할 수 있지만, hash Join은 사용하지 못한다. NL 조인의 경우 인덱스를 활용하여 효율적인 탐색이 가능하고,
>sort merge의 경우 인덱스가 존재한다면 시스템에 따라 정렬을 하지 않아도 되는 경우가 있어 효율적으로 동작할 수 있다.
