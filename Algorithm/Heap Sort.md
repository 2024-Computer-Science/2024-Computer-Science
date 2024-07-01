- **완전 이진 트리**와 **힙(Heap) 자료구조**를 기반으로한 정렬 방식
    - 완전 이진 트리 
        : 삽입할 때 왼쪽부터 차례대로 추가하는 이진 트리
        

- 정렬 과정
    1. 최대 힙을 구성
    2. 현재 힙 루트는 가장 큰 값이 존재함. 루트의 값을 마지막 요소와 바꾼 후, 힙의 사이즈 하나 줄임
    3. 힙의 사이즈가 1보다 크면 위 과정 반복
    
- 시간 복잡도
    
    최대 힙으로 만드는 과정(heapify)의 시간 복잡도는 O(logn) 이다.
    
    이 heapify의 과정이 n개의 원소를 다 정렬할 때까지 반복되므로 최종 힙 정렬의 시간 복잡도는 **O(nlogn)** 이 된다.
    
- 구현
    
    ```python
    # 힙 정렬
    def heapify(unsorted, index, heap_size):
        # 최대 힙을 유지하는 함수
        largest = index  # 현재 노드를 가장 큰 값으로 가정
        left = 2 * index + 1  # 왼쪽 자식 노드의 인덱스 계산
        right = 2 * index + 2  # 오른쪽 자식 노드의 인덱스 계산
    
        # 왼쪽 자식 노드가 존재하고, 자식 노드의 값이 현재 노드의 값보다 큰 경우
        if left < heap_size and unsorted[left] > unsorted[largest]:
            largest = left
    
        # 오른쪽 자식 노드가 존재하고, 자식 노드의 값이 현재 노드의 값보다 큰 경우
        if right < heap_size and unsorted[right] > unsorted[largest]:
            largest = right
    
        # 가장 큰 값이 현재 노드의 값이 아닌 경우
        if largest != index:
            # 현재 노드와 가장 큰 값을 교환
            unsorted[largest], unsorted[index] = unsorted[index], unsorted[largest]
            # 교환된 자식 노드에 대해 재귀적으로 heapify를 호출
            heapify(unsorted, largest, heap_size)
    
    def heap_sort(unsorted):
        # 힙 정렬 함수
        n = len(unsorted)  # 배열의 길이 계산
    
        # 힙을 구성하는 과정 (배열을 최대 힙으로 변환)
        for i in range(n // 2 - 1, -1, -1):
            heapify(unsorted, i, n)
    
        # 정렬 과정
        for i in range(n - 1, 0, -1):
            # 힙의 루트(가장 큰 값)와 현재 마지막 요소를 교환
            unsorted[0], unsorted[i] = unsorted[i], unsorted[0]
            # 힙 크기를 줄이고, 루트 노드에 대해 heapify 호출
            heapify(unsorted, 0, i)
    
        return unsorted  # 정렬된 배열 반환
    
    ```
