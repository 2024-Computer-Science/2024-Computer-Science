# 트라이(Trie)

### 트라이

문자열을 저장하고 효율적으로 탐색하기 위한 트리 형태의 자료구조

re’trie’val tree에서 파생된 단어

![Untitled](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/7ca1b12f-87bc-4977-9641-7c684ae5fbc2)


(검색할 때 사용하는 자동완성, 사전 검색 등… 문자열 탐색에 특화)

### 트라이(Trie) 장단점

<장점>

1. 문자열 검색을 빠르게 할 수 있다.
    
    (BST에서 문자열의 최대 길이가 M이라고 할 때, 검색하는 시간 복잡도는 O(M*logN), 그러나 Trie에서는 O(M)으로 가능)
    

<단점>

1. 각 노드에서 자식들에 대한 포인터들을 배열로 모두 저장하고 있어서 저장 공간의 크기가 크다. (공간 복잡도가 큼)

### 트라이 예제(동작 방식)

<aside>
💡 [https://velog.io/@kimdukbae/자료구조-트라이-Trie](https://velog.io/@kimdukbae/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%8A%B8%EB%9D%BC%EC%9D%B4-Trie)

</aside>
