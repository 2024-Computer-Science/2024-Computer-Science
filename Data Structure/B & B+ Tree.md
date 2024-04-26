# B & B+ Tree

### B & B+ Tree

- 데이터베이스, 파일 시스템에서 index에 자주 사용되는 Balanced Tree종류 중 하나인 자료구조
- MySQL의 InnoDB 스토리지 엔진이 주로 B+ Tree를 사용

### B+Tree의 특징

![Untitled](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/bcdbd720-e05f-4b61-ac6f-bda48352bf86)

![Untitled 1](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/a4a56a37-680d-44c0-abb9-0fbf86aa0302)

![Untitled 2](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/34a5911a-60fd-491c-aac8-c83a62345404)

1. 루트 노드는 적어도 2개 이상의 자식을 가져야 한다.
2. 루트 노드를 제외한 모든 노드는 **M/2개부터 M개의 자식**을 가진다.
3. 노드에는 최소 [M/2]-1개부터 최대 M-1개의 키를 포함한다
**([M/2]-1 < key < M-1)**
4. 노드의 key(자료)의 갯수가 x개라면, 자식은 x+1개여야 한다.
5. 최소 차수(t)는 자식 수의 하한 값을 의미한다.
    
    (ex. let t = 2,, M = 2 * t - 1)
    
6. 자료의 중복은 없다.

### B Tree와 B+ Tree의 차이점

- B+ Tree는 모든 data가 leaf node에만 모여있다.
    
    (B Tree의 경우 각 노드(key)마다 data를 저장)
    
- 모든 리프노드가 연결 리스트로 연결
    
    (B Tree는 옆에 있는 리프 노드를 검사하기 위해 다시 루트 노드부터 검사해야 하지만, B+ 트리는 리프 노드에서 연결리스트로 연결되어있기 때문에 형제노드를 선형 검사 할 수 있어서 시간복잡도가 굉장히 줄어들었다.)
