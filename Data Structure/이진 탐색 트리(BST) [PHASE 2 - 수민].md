### 💡 이진 탐색 트리: 이진 탐색 + 연결리스트
이진 탐색에서 탐색에 소요되는 시간복잡도 O(logN)
연결리스트에서 삽입,삭제의 시간복잡도 O(1)
따라서 이진탐색과 연결리스트의 장점을 활용하기 위해 **이진 탐색 트리를 사용하자!**

![image](https://github.com/user-attachments/assets/e7513e01-b16d-49ba-bbaa-aa3b64193faa)

### ⭐️ 특징

- 이진 트리의 특징 : 각 노드의 자식이 **최대 2개**
- 각 노드의 왼쪽 자식은 부모보다 작다.
- 각 노드의 오른쪽 자식은 부모보다 크다.
- 중복된 노드는 없어야 한다.


> 💡 중복이 많은 트리는 검색 속도를 느리게 한다. 중복이 많은 경우 노드에 count값을 가지게 하여 처리하는 것이 효율적이다.



> 💡 편향된 트리는 시간복잡도 O(N)을 가지기 때문에 이진 탐색 트리의 이점이 없다. 이를 위해 AVL Tree 혹은 Red Black Tree, b tree등을 이용한다.


### ⭐️ 시간 복잡도

**O(h)**

삽입, 검색, 삭제 시간복잡도는 **트리의 높이**에 비례하다.

### ⭐️ 탐색 과정

1. 루트 노드와 찾고자하는 값을 비교한다. 찾고자하는 값이면 종료
2. 찾고자 하는 값이 루트 노드보다 작으면 왼쪽 서브트리로 탐색
3. 찾고자 하는 값이 루트 노드보다 크다면 오른쪽 서브트리로 탐색

이런 탐색 과정을 거치면 최대 트리 높이인 h만큼 탐색이 진행된다. (찾고자 하는 값이 리프노드일 때, 혹은 찾고자 하는 값이 없을 때)

### ⭐️삽입 과정

1. 루트 노드와 비교해 같다면 오류 ( 중복 X)
2. 루트 노드보다 작다면 왼쪽 서브트리를 탐색, 비어있다면 추가하고, 비어있지 않다면 값을 비교
3. 루트 노드보다 크다면 오른쪽 서브트리를 탐색, 비어있다면 추가하고, 비어있지 않다면 값을 비교

### ⭐️삭제 과정

3가지 상황을 고려해야한다. 

1. 삭제하고자 하는 노드가 리프노드일 경우
    
    부모 노드의 자식 노드를 NULL로 만들어주고, 해당 노드 삭제
    
2. 삭제하고자 하는 노드의 서브트리가 하나인 경우
    
    삭제할 노드의 자식 노드를 삭제할 노드의 부모노드가 가리키도록 하고, 해당 노드 삭제
    
3. 삭제하고자 하는 노드의 왼쪽,오른쪽 서브트리 모두 존재할 경우
    1. 삭제할 노드의 왼쪽 서브 트리의 가장 큰 자손을 해당 노드 자리에 올리기 혹은
    2. 삭제할 노드의 오른쪽 서브 트리의 가장 작은 자손을 해당 노드 자리에 올리기

### ⭐️ 구현

```sql
    public class Node {
        private int data;
        private Node left;
        private Node right;

        public Node(int data) {
            this.setData(data);
            setLeft(null);
            setRight(null);
        }

        public int getData() {
            return data;
        }

        public void setData(int data) {
            this.data = data;
        }

        public Node getLeft() {
            return left;
        }

        public void setLeft(Node left) {
            this.left = left;
        }

        public Node getRight() {
            return right;
        }

        public void setRight(Node right) {
            this.right = right;
        }
    }

    public Node root;

    public binarySearchTree() {
        this.root = null;
    }

    //탐색 연산
    public boolean find(int id) {
        Node current = root;
        while (current != null) {
            //현재 노드와 찾는 값이 같으면
            if (current.getData() == id) {
                return true;
                //찾는 값이 현재 노드보다 작으면
            } else if (current.getData() > id) {
                current = current.getLeft();
                //찾는 값이 현재 노드보다 크면
            } else {
                current = current.getRight();
            }
        }
        return false;
    }

    //삭제 연산
    public boolean delete(int id) {
        Node parent = root;
        Node current = root;
        boolean isLeftChild = false;
        
        //일단 해당 id를 가진 노드를 찾음
        while (current.getData() != id) {
            parent = current;
            if (current.getData() > id) {
                isLeftChild = true;
                current = current.getLeft();
            } else {
                isLeftChild = false;
                current = current.getRight();
            }
            if (current == null) {
                return false;
            }
        }
        
        //Case 1: 자식노드가 없는 경우 -> 해당 노드만 삭제 해주면 된다. 부모와의 연결을 끊음
        if (current.getLeft() == null && current.getRight() == null) {
            if (current == root) {
                root = null;
            }
            if (isLeftChild == true) {
                parent.setLeft(null);
            } else {
                parent.setRight(null);
            }
        }
        //Case 2 : 하나의 자식을 갖는 경우. 내 부모와 내 자식 노드를 연결시켜준다.
        else if (current.getRight() == null) {
            if (current == root) {
                root = current.getLeft();
            } else if (isLeftChild) {
                parent.setLeft(current.getLeft());
            } else {
                parent.setRight(current.getLeft());
            }
        } else if (current.getLeft() == null) {
            if (current == root) {
                root = current.getRight();
            } else if (isLeftChild) {
                parent.setLeft(current.getRight());
            } else {
                parent.setRight(current.getRight());
            }
        }
        //Case 3 : 두개의 자식을 갖는 경우
        else if (current.getLeft() != null && current.getRight() != null) {
            // 여기서는 오른쪽 자식 노드에서 가장 작은 값을 올리도록 함
            Node successor = getSuccessor(current);  //오른쪽 서브트리에서 에서 가장 작은 값 찾기
            if (current == root) {
                root = successor;
            } else if (isLeftChild) { //삭제할 노드가 왼쪽 자식인 경우, 왼쪽자식을 후계자로 지정. 원래있던놈은 지워짐
                parent.setLeft(successor);
            } else { //오른쪽 자식일 경우, 오른쪽 자식을 후계자로 지정. 원래있던놈은 지워짐
                parent.setRight(successor);
            }
            successor.setLeft(current.getLeft()); //후계자의 왼쪽 자식은 지우고자하는 노드의 왼쪽 자식으로 설정해줌
        }
        return true;
    }
		
		
		//오른쪽 자식노드에서 가장 작은 값 = 후계자 찾기
    public Node getSuccessor(Node deleleNode) {
        Node successsor = null;
        Node successsorParent = null;
        Node current = deleleNode.getRight(); //오른쪽 자식 노드
        while (current != null) {
            successsorParent = successsor;
            successsor = current; //현재 후계자는 오른쪽 자식 노드
            current = current.getLeft(); //서브트리의 가장 작은 값은 무조건 가장 왼쪽 값임
        }
        //후계자가 삭제하고자하는 노드의 바로 오른쪽 노드일 경우에는, 이과정이 필요없다. 그림 2 보기
        if (successsor != deleleNode.getRight()) {
            successsorParent.setLeft(successsor.getRight());
            successsor.setRight(deleleNode.getRight());
        }
        return successsor;
    }

    //삽입 연산
    public void insert(int id) {
        Node newNode = new Node(id);
        if (root == null) {
            root = newNode;
            return;
        }
        Node current = root;
        Node parent = null;
        while (true) {
            parent = current;
            if (id < current.getData()) {
                current = current.getLeft();
                if (current == null) {
                    parent.setLeft(newNode);
                    return;
                }
            } else {
                current = current.getRight();
                if (current == null) {
                    parent.setRight(newNode);
                    return;
                }
            }
        }
    }
```
