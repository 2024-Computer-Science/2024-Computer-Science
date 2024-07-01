- **안정 정렬**에 속하며, **분할 정복 알고리즘**의 하나 이다.
    - 안정 정렬
        
        : 동일한 값을 가진 데이터들의 순서가 원래의 순서와 같이 유지되는 정렬 방법
        
        : 예시)
        
        `list=[1, 7, 3, 5, 4, 7, 9]`
        
        이 리스트를 정렬했을 때
        
        (1) `list=[1, 3, 4, 5, 7(1), 7(2), 9`
        
        (2) `list=[1, 3, 4, 5, 7(2), 7(1), 9`
        
        (1)처럼 나오면 안정(Stable) 정렬,
        
        (2)처럼 나오면 불안정(Unstable) 정렬이라고 한다.
        
    - 분할 정복(divide and conquer) 알고리즘
    : 문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략이다. 분할 정복 방법은 대개 순환 호출을 이용하여 구현한다.

- **시간복잡도**
    
    : O(n log n)
    

- 정렬 방법
    
    **1. 주어진 리스트를 절반으로 분할하여 부분리스트로 나눈다. (Divide : 분할)**
    
    **2. 해당 부분리스트의 길이가 1이 아니라면 1번 과정을 되풀이한다.**
    
    **3. 인접한 부분리스트끼리 정렬하여 합친다. (Conqure : 정복)**
    
    ![image](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/78026977/77723ac9-3213-41e2-a901-761a530c927e)


- 구현
    - mergeSort(): 배열을 반으로 나누어 주는 함수
    - merge(): 반으로 나누어준 함수를 갖고 정렬해 새로운 배열로 만들어주는 함수
    
    ```python
    # 재귀를 이용한 합병 정렬 함수 정의
    def merge_sort(arr):
        # 종료 조건은 배열의 길이가 0 또는 1일 때
        if len(arr) <= 1:
            return arr
    
        # 절반으로 나누어 왼쪽 배열과 오른쪽 배열로 분할
        mid = len(arr) // 2
        left_half = arr[:mid]
        right_half = arr[mid:]
    
        # 아까 나눈 왼쪽 배열과 오른쪽 배열을 각각 다시 호출
        left_half = merge_sort(left_half)
        right_half = merge_sort(right_half)
    
        # 왼쪽 배열과 오른쪽 배열을 합병한 것을 반환
        return merge(left_half, right_half)
    
    # 합병 함수 정의
    def merge(left_half, right_half):
        # 반환할 배열과 왼쪽 절반과 오른쪽 절반에 대한 인덱스 초기화
        result = []
        i = j = 0
    
        # 왼쪽 절반이나 오른쪽 절반 중 인덱스가 초과할 때까지 반복
        while i < len(left_half) and j < len(right_half):
            if left_half[i] < right_half[j]:
                result.append(left_half[i])
                i += 1
            else:
                result.append(right_half[j])
                j += 1
    
        # 위의 루프에서 초과했을 경우 남은 부분 배열을 모두 더함
        result += left_half[i:]
        result += right_half[j:]
    
        # 정렬된 배열 반환
        return result
    
    # 테스트 코드
    if __name__ == "__main__":
        array = [6, 5, 3, 1, 8, 7, 2, 4]
        print(array)
        print(merge_sort(array))
    ```
    
- 장점
    1. 시간 복잡도 O(nlogn)으로 굉장히 빠름
    2. 서로 떨어져 있는 것을 교환 하는게 아니라서 안정적인 정렬
- 단점
    1. 임시의 배열 필요하므로, 추가 메모리 요구
