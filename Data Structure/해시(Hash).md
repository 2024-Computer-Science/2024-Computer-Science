# 해시(Hash)

### 해시

임의의 길이의 데이터를 특정 해시 함수(hash function)에 따라서 고정된 길이의 데이터(해시 값)로 매핑하는 방법

![Untitled](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/d45a60cc-1f2a-40c0-ac52-b65a02452b21)


```jsx
Lee → 해싱함수 → 5
Kim → 해싱함수 → 3
Park → 해싱함수 → 2
...
Chun → 해싱함수 → 5 // Lee와 해싱값 충돌
```

### 해시 테이블의 구성 요소

1. Key : 고유한 값. hash fucntion의 input값
2. Hash Function : Key를 고정된 길이의 hash로 변경해주는 함수
3. Value : 저장소(bukets or slot)에 최종적으로 저장되는 값.
4. hash Table : 해시함수를 사용하여 키를 해시값으로 매핑하고, 이 값을 주소 또는 색인(index)삼아 데이터를 key와 함께 저장하는 자료 구조

### 해시의 문제점

- 저장할 수 있는 공간이 한정되어 있다보니 해시 충돌(hash collision)이 발생한다.
    - 추후에 나올 “개방 주소법(Open Addressing)” , “체이닝(Chaining)”과 같은 방법을 통해 개선
- 순서/관계가 있는 배열에 어울리지 않는다.
    - 해시 함수를 통해 변환하여 저장하기 때문에 순서/관계가 보장되지 않는다.
- Hash Function에 대한 의존도가 높다.

### Driect-address table

키의 전체 개수와 동일한 크기의 버킷(저장소)를 가지는 해시 테이블

→ 1:1 매칭이 되기 때문에 해시 충돌이 생기지 않지만, 보통은 실제 키보다 적은 해시테이블을 사용하기 때문에, 추후에 소개되는 다양한 방법을 통해서 해시 충돌(Collision)을 해결할 수 있다.

### 해시 충돌

- Hash Table보다 Key값이 더 많은 이유때문에 저장 시 충돌이 발생하는 현상

### 해시 충돌 해결 방법

1. Chaining
- 저장소에 충돌(Collision)이 발생하면 기존 값 뒤에 새로운 연결리스트를 생성하여 연결하는 방식

![Untitled 1](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/645535f4-7d8e-43f7-b455-321bb2d33e17)


<장점>

1. 미리 충돌을 대비해서 공간을 많이 잡아놓을 필요가 없다.

<단점>

1. 같은 Hash에 많은 자료들이 체이닝으로 연결되면 검색 시 효율이 낮아진다.
2. 충돌이 많이 날 경우 계속 리스트가 연결되므로 메모리 문제가 생길 수 있다.

1. Open Addressing(개방 주소법)
- 충돌이 일어나면 비어있는 Hash Table에 데이터를 저장하는 방법.
    
    (이 때, 비어있는 Hash Table을 찾아가는 방법은 여러가지가 있음)
    
    ![Untitled 2](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/48d5ae73-d53c-4330-a647-59975f0cdc6d)

    
    - 선형 탐색 : 해시 값에서 고정 폭으로 건너 뛰면서 비어있는 해시가 나오면 저장
        
        ![Untitled 3](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/a5a8c468-f05b-46bc-8f91-c571fe3f579e)

        
    - 제곱 탐색 : 해시 값에서 고정 폭을 제곱수로 건너 뛰면서 비어있는 해시가 나오면 저장
        
        ![Untitled 4](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/81a5f183-87de-42c6-b6ee-b6272b5acb42)

        
        - (ex. 1 → 4 → 9 → 16 → …)

### Hash Function 매핑 개선

좋은 해시함수란, 특정 값에 치우지지 않고 고르게 만드는 함수가 좋은 해시함수라 할 수 있다.

- Division method
    - 가장 기본적인 해시 함수
    - 숫자로 된 key를 해시 테이블의 크기 m으로 나눈 나머지를 해시 값으로 변환
    - 간단하면서도 빠른 연산이 장점
    - 해시의 중복을 방지하기 위해 테이블의 크기 m은 소수(prime number)로 지정해서 사용하는 것이 좋다.
    - 하지만 남는 공간의 발생때문에 메모리상으로 비효율적임.
- Multiplication method
    - 숫자 키 k, A는 0<A<1 사이의 실수 일 때, ‘hash function(k) = (k*a mod 1) * m’으로 계산
    - 이진수 연산에 최적화된 컴퓨터 구조를 고려한 해시 함수
- Univesal hashing
    - 여러 개의 해시 함수를 만들고, 이 해시 함수의 집합 H에서 무작위로 해시함수를 선택해 해시 값을 만드는 기법
    - 서로 다른 해시함수가 서로 다른 해시 값을 만들어내기 때문에 같은 공간에 매핑할 확률을 줄이는 것이 목적
    - 즉, 많은 해시 함수를 랜덤하기 뽑는 방법

### 해시 버킷 동적 확장

- 해시 버킷의 크기가 충분히 크다면 Collision 발생 빈도를 낮출 수 있다. 하지만 메모리는 한정되어 있기 때문에 무작정 크게 할당할 수는 없다. 따라서 load factor(해시가 얼마나 차있는지에 대한 수)가 일정 수준 이상(0.7~0.8)이라면 해시 버킷의 크기(m)을 확장시키는 동적 확장 방식을 사용하기도 한다. → 이 때 “리해싱”과정을 거침

<aside>
💡 Load Factor : 할당된 키의 개수 / 해시 버킷의 크기
Rehashing : 기존 저장되어있는 값들을 다시 해싱하여 새로운 키를 부여

</aside>
