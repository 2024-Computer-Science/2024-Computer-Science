# Tree

트리 : 그래프의 일종으로 정점(Vertex)과 간선(Edge)을 이용하여 데이터의 배치를 추상화 한 자료구조.

![image](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/47886678-613f-4891-b9c2-117e02993655)


### 트리의 구성 요소

1. 노드(Node) : 데이터와 다른 정점을 참조할 공간
2. 정점(Vertex) : 간선으로 연결할 수 있는 각각의 노드
3. 간선(Edge) : 정점과 다른 정점을 연결하는 개념

### 정점의 분류

1. 뿌리(Root) : 트리 자료구조의 가장 상위에 위치한 노드
2. 가지(Branch) : 루트와 잎 사이에 존재하는 모든 노드
3. 잎(Leaf) : 가지 끝에 매달려 있는 가장 아래에 위치한 노드

### 노드 종류

1. 부모(Parent) : 특정 노드 위에 있는 노드
2. 자식(Childeren) : 특정 노드 밑에 있는 노드
3. 형제(Sibling) : 공통된 부모를 가지고 있는 노드

### 알아야 할 개념들

1. 깊이(Depth) : 루트 노드에서 해당 노드까지 최단 경로의 길이
2. 레벨(Level) : 깊이가 같은 노드 집합
3. 높이(Height) : 가장 깊은 곳에 있는 Leaf Node의 깊이
4. 차수(Degree) : 특정 노드의 자식 개수.
5. 트리의 차수(Degree of Tree) : 트리 내에 있는 노드들 중 가장 자식노드가 많은 노드의 차수

---

### 노드로 트리를 표현하는 방법

1. N-Link 표현법 : 노드 내에 n의 크기를 가진 자식 배열로 트리를 구현하는 방법
2. Left Child - Right Sibling 표현법 : 왼쪽에는 자식노드에 대한 정보만, 오른쪽에는 형제 노드에 대한 정보만 가지고 트리를 구현하는 방법
    
![Untitled 1](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/2ab576a1-4da5-431d-81c7-5ec1586fbf22)


    
    <aside>
    💡 <Left Child - Right Sibling 표현법 참고자료>
    [https://rooftoproom-whale.tistory.com/23#노드로 표현하기-1](https://rooftoproom-whale.tistory.com/23#%EB%85%B8%EB%93%9C%EB%A1%9C%20%ED%91%9C%ED%98%84%ED%95%98%EA%B8%B0-1)
    
    </aside>
    

### 트리의 특징

1. 트리에는 사이클이 존재할 수 없다. (만약 존재한다면 트리가 아니라 그래프임.)
2. 모든 노드는 자료형으로 표현이 가능하다
3. 루트에서 한 노드로 가는 경로는 유일한 경로뿐이다. (1과 동일한 내용)
4. 노드의 개수가 N개이면, 간선의 개수는 N-1개를 가진다.

<aside>
💡 <그래프와 트리의 차이>
1. 사이클의 유무(사이클이 있으면 그래프, 없으면 트리)
* 그러나 사이클이 존재하지 않는 그래프는 무조건 트리??? → X
(사이클이 존재하지 않는 그래프 → Forest
트리는 싸이클이 존재하지 않으면서 모든 노드가 간선으로 이어져 있어야 한다.)

</aside>

### 트리 순회 방식

![Untitled 2](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/7dee15ab-4dff-490e-8898-bf53e7279d41)


1. 전위 순회(Pre-order)

각 부모 노드를 순차적으로 먼저 방문하는 방식

(부모 → 왼쪽 자식 → 오른쪽 자식)

![Untitled 3](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/074cb550-ff9f-4dbe-90f4-931a57de6ffc)


2. 중위 순회(In-order)

왼쪽 하위 트리를 방문 후 부모 노드를 방문하는 방식

(왼쪽 자식 → 부모 → 오른쪽 자식)

![Untitled 4](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/31862bf3-ce5a-4e5a-b1e0-0b68d45e8cd5)


3. 후위 순회(Post-order)

왼쪽 하위 트리부터 하위를 모두 방문 후 부모 노드를 방문하는 방식

(왼쪽 자식 → 오른쪽 자식 → 부모)

### 트리의 종류

1. Binary Tree(이진 트리)
    
![Untitled 5](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/e1da525e-a2bf-418d-835e-172ddc9f98a7)

    
    - Ternary tree : 자식이 최대 3개인 트리
    - Binary tree : 자식이 최대 2개인 트리
    
2. Balanced Tree
    
![Untitled 6](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/6d348b3c-b3bc-4db3-9526-96b635b6d662)

    
    - Balanced tree : Left, Right 노드 갯수가 비슷한 트리
    - Unbalanced tree : 한 쪽으로 지나치게 치우쳐진 트리

3. Binary Serach Tree (이진 탐색 트리)
    
![Untitled 7](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/4f3a1582-1a8c-4559-b600-6bdc9ab1432c)

    
    - Binary tree : 이진 트리 중 부모를 기준으로 노드의 숫자가 자유로운 이진 트리
    - Binary Search tree : Left child와 그 이하 노드들의 Data가 부모 노드의 데이터보다 작아야 하고, Right child와 그 이하 노드들의 데이터가 부모 노드의 데이터보다 커야 한다.
        
        (즉, 중위 순위(In-order)를 돌았을 때, 값이 오름차순으로 정렬되서 나오면 BST)
        
    - Complete Binary tree : 마지막 레벨을 제외한 모든 서브 트리의 레벨이 같아야 하고, 마지막 레벨은 Left child부터 채워져 있는 트리
        
        (즉, 레벨이 모두 동일하고, 왼쪽부터 채워져 있는 트리)
        
    - Full Binary tree : 자식 노드가 아예 없거나, 최대 두 개인 트리
        
        (자식노드가 하나면 안됨.)
        
    
4. Perfect Bianry tree
        
![Untitled 8](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/cd363d0c-5958-4459-ba68-83b9b551d90b)

        
    - Perfect Binary tree : 완벽한 피라미드 형태로, 모든 노드의 자식이 2개씩 있는 트리
        
        (이 때, 노드의 갯수 : $2^h-1$)
