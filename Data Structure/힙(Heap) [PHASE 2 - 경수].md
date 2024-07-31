# 힙(Heap)

# 힙(Heap)

→ 우선순위 큐를 위해 만들어진 자료구조. 완전 이진 트리의 일종으로, 최대 또는 최소 값을 빠르게 찾아낼 수 있다.

![Untitled](https://github.com/user-attachments/assets/68c18fdd-dd9a-49ce-b080-314f4db9e3bc)


<aside>
❓ 우선순위 큐(Priority Queue)
데이터들의 우선 순위를 가지고 있고, 우선 순위대로 데이터가 빠져나가는 자료 구조

</aside>

## 힙 종류

### 최대 힙(Max Heap)

- 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리.
- Root에 가장 큰 값이 존재.

### 최소 힙(Min Heap)

- 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리.
- Root에 가장 작은 값이 존재.

<삽입 & 삭제>

![image](https://github.com/user-attachments/assets/872be3ba-954a-4869-9c60-7e6a70ddc3f6)


![images_hwamoc_post_534fd918-a1d1-431f-b08c-46dc507cae35_%E1%84%92%E1%85%B5%E1%86%B82](https://github.com/user-attachments/assets/ea970f41-9837-4422-b747-a3c939d10439)


[삽입]
해당 값이 빠져나가면, 힙의 마지막 노드를 Root로 올리고 아래로 비교하면서 힙을 재구성.

[삭제]

새로운 값이 들어오면, 힙의 마지막 노드에 삽입한 후, 새로운 노드를 부모 노드와 비교하며 힙을 재구성
