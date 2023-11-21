---
title:  "[비선형 자료구조] 이진 탐색 트리"
category: dataStructure
typora-root-url: ../
toc: true
toc_sticky: true
use_math: true
---

## <br>이진 탐색 트리(Binary Search Tree)

아래의 규칙으로 구성 된 이진 트리

- 왼쪽 자식 노드의 키는 부모 노드의 키보다 작음
- 오른쪽 자식 노드의 키는 부모 노드의 키보다 큼
- 각각의 서브 트리도 이진 탐색  트리를 유지
- 중복된 키를 허용하지 않음

![bST](/images/2023-11-22-algorithm-BinarySearchTree/bST.png)



### <br>이진 탐색 트리의 특징

- 이진 탐색 트리 규칙에 의해 데이터가 정렬됨

- 이진 트리에 비해 탐색이 빠름(균형 유지 필요)
  - 시간복잡도 : 균형상태 -  O(logN) / 비균형상태 - O(N)



### <br>이진 탐색 트리 - 탐색

- 찾고자 하는 데이터를 루트 노드부터 비교 시작
- 대소 비교를 하여 찾는 데이터가 작으면 왼쪽, 크면 오른쪽 노드로 이동
- 찾는 데이터가 없으면 null 반환
- 어떤 데이터를 찾더라도 최대 트리 높이 만큼의 탐색이 이루어짐

<img src="/images/2023-11-22-algorithm-BinarySearchTree/search.png" alt="search" style="zoom:80%;" />



### <br>이진 탐색 트리 - 삽입

- Root부터 비교 시작 (중복 키 발견 시 노드 추가하지 않고 종료)
- 삽입할 키가 현재 노드의 키보다 작으면 왼쪽으로 크면 오른쪽으로 이동
- Leaf 노드에 도달 후 키 비교하여 작으면 왼쪽 크면 오른쪽에 삽입

<img src="/images/2023-11-22-algorithm-BinarySearchTree/insert.png" alt="insert" style="zoom:80%;" />

### <br>이진 탐색 트리 - 삭제

- 삭제 대상 노드가 leaf 노드인 경우

  - 삭제 대상 노드 삭제

  - 부모 노드의 해당 자식 링크 null로 변경

![delete1](/images/2023-11-22-algorithm-BinarySearchTree/delete1.png)



<br>

- 삭제 대상 노드에 자식 노드가 하나 있는 경우
  - 자식 노드를 삭제 대상 노드의 부모 노드에 연결
  - 삭제 대상 노드 삭제

![delete2](/images/2023-11-22-algorithm-BinarySearchTree/delete2.png)

<br>

- 삭제 대상 노드에 자식 노드가 둘인 경우
  - i) 삭제 대상 노드에서 왼쪽 서브 트리에서 가장 큰 노드 선택
  - ii)  삭제 대상 노드의 오른쪽 서브 트리에서 가장 작은 노드 선택
  - i 또는 ii에서 선택한 노드를 삭제 대상 노드 위치로 올림
  - 위로 올리는 과정에서 다른 자식노드들의 링크 연결작업 진행 후 삭제 대상 노드 삭제 

<img src="/images/2023-11-22-algorithm-BinarySearchTree/delete3.png" alt="delete3" style="zoom:80%;" />





### <br>이진 탐색 트리 구현(List)

```java
class Node {
    int key;
    Node left;
    Node right;

    Node(int key, Node left, Node right) {
        this.key = key;
        this.left = left;
        this.right = right;
    }
}

class BinarySearchTree {
    Node head;

    BinarySearchTree(int key) {
        this.head = new Node(key, null, null);
    }

    //데이터 추가
    public void addNode(int key) {
        if (this.head == null) {
            this.head = new Node(key, null, null);
        } else {
            Node cur = this.head;

            while (true) {
                Node pre = cur;
                if (key < cur.key) {
                    cur = cur.left;

                    if (cur == null) {
                        pre.left = new Node(key, null, null);
                        break;
                    }
                } else {
                    cur = cur.right;

                    if (cur == null) {
                        pre.right = new Node(key, null, null);
                        break;
                    }
                }
            }
        }
    }

    //데이터 삭제
    public void removeNode(int key) {
        Node parent = null;         // 부모 노드
        Node successor = null;      // 지우고 변경해줘야하는 후계자를 가리킬 변수
        Node predecessor = null;    // successor 의 부모를 가리킬 노드
        Node child = null;          // successor의 자식노드 여부를 확인할 변수

        Node cur = this.head;
        while (cur != null) {
            if (key == cur.key) {
                break;
            }

            parent = cur;
            if (key < cur.key) {
                cur = cur.left;
            } else {
                cur = cur.right;
            }
        }

        if (cur == null) {
            System.out.println("key에 해당하는 노드가 없습니다.");
            return;
        }
        // Leaf 노드인 경우
        if (cur.left == null && cur.right == null) {
            if (parent == null) { //트리에 노드 1개바께 없는 경우
                this.head = null;
            } else {
                if (parent.left == cur) {
                    parent.left = null;
                } else {
                    parent.right = null;
                }
            }
        }
        // 자식 노드가 하나인 경우
        else if (cur.left != null && cur.right == null || cur.left == null && cur.right != null) {
            if (cur.left != null) {
                child = cur.left;
            } else {
                child = cur.right;
            }

            if (parent == null) {   //루트노드인데 자식노드가 1개만 있는 경우
                this.head = child;
            } else {
                if (parent.left == cur) {
                    parent.left = child;
                } else {
                    parent.right = child;
                }
            }
        } else { // 자식 노드가 둘인 경우(좌측에서 가장 큰 노드를 찾기)
            predecessor = cur;
            successor = cur.left;

            while (successor.right != null) {
                predecessor = successor;
                successor = successor.right;
            }

            predecessor.right = successor.left;
            successor.left = cur.left;
            successor.right = cur.right;

            if (parent == null) {
                this.head = successor;
            } else {
                if (parent.left == cur) {
                    parent.left = successor;
                } else {
                    parent.right = successor;
                }
            }
        }
    }
}
```

### <br>이진 탐색 트리 구현(재귀)

```java
class Node {
    int key;
    Node left;
    Node right;

    Node(int key, Node left, Node right) {
        this.key = key;
        this.left = left;
        this.right = right;
    }
}

class BinarySearchTree {
    Node head;
    
    
    BinarySearchTree(int key) {
        this.head = new Node(key, null, null);
    }
    
    //데이터 추가
    public Node addNodeRecursive(Node cur, int key) {
        if (cur == null) {
            return new Node(key, null, null);
        }

        if (key < cur.key) {
            cur.left = addNodeRecursive(cur.left, key);
        }else {
            cur.right = addNodeRecursive(cur.right,key);
        }

        return cur;
    }
    
    //데이터 삭제
    public Node removeNodeRecursive(Node cur, int key) {
        if (cur == null) {
            return null;
        }

        if (key < cur.key) {
            cur.left = removeNodeRecursive(cur.left, key);
        } else if (key > cur.key) {
            cur.right = removeNodeRecursive(cur.right, key);
        } else {
            if (cur.left == null) {
                return cur.right;
            } else if (cur.right == null) {
                return cur.left;
            } else {
                Node predecessor = cur;
                Node successor = cur.left;

                while (successor.right != null) {
                    predecessor = successor;
                    successor = successor.right;
                }

                predecessor.right = successor.left;
                cur.key = successor.key;
            }
        }
        return cur;
    }
    
}
```





### <br>균형 이진 탐색 트리

- Balanced Binary Search Tree
- 노드의 삽입와 삭제가 일어날 때 균형을 유지하도록 하는 트리
  - 데이터의 삽입에 따라 편향트리(a)가 될 수도 있는데 이것을 이진 탐색 트리(b)로 조정
- AVL 트리, Red-Black 트리

<img src="/images/2023-11-22-algorithm-BinarySearchTree/BBST.png" alt="BBST" style="zoom:80%;" />



### <br>AVL 트리

- 노드가 삽입, 삭제될 때 균형을 체크하고 유지하는 트리
- 각 노드의 BF를 [-1,0,1] 만 가지게 하여 균형을 유지
- BF(Balance Factor) : 왼쪽 서브트리 높이 - 오른쪽 서브트리 높이



### <br>AVL 트리 - 리밸런싱

- 균형이 깨진 경우
  - BF가 '+' 이면 왼쪽 서브트리에 이상 있음
  - BF가 '-' 이면 오른쪽 서브트리에 이상 있음
- 회전 연산
  - 단순 회전 : LL, RR
  - 이중 회전 : LR, RL



#### AVL 트리 - LL(Left-Left)

- 오른쪽 방향으로 1회 회전

<img src="/images/2023-11-22-algorithm-BinarySearchTree/LL.png" alt="LL" style="zoom: 80%;" />



#### <br>AVL 트리 - RR(Right-Right)

- 왼쪽 방향으로 1회 회전

<img src="/images/2023-11-22-algorithm-BinarySearchTree/RR.png" alt="RR" style="zoom:48%;" />

#### <br>AVL 트리 LR(Left-Right)

- RR 회전 후 LL 회전

![LR](/images/2023-11-22-algorithm-BinarySearchTree/LR.png)

#### <br>AVL 트리 RL(Right-Left)

- LL회전 후 RR 회전

![RL](/images/2023-11-22-algorithm-BinarySearchTree/RL-1700578098157-8.png)



### <br>AVL 트리 구현

```java
class Node {
    int key;
    int height;
    Node left;
    Node right;

    public Node(int key, Node left, Node right) {
        this.key = key;
        this.height = 0;
        this.left = left;
        this.right = right;
    }
}

class AVLTree {
    Node head;

    //높이 정보
    public int height(Node node) {
        if (node == null) {
            return -1;
        }
        return node.height;
    }

    // LL case
    public Node rightRotate(Node node) {
        Node lNode = node.left;

        node.left = lNode.right;
        lNode.right = node;

        node.height = Math.max(height(node.left), height(node.right)) + 1;
        lNode.height = Math.max(height(lNode.left), height(lNode.right)) + 1;

        return lNode;
    }

    // RR case
    public Node leftRotate(Node node) {
        Node rNode = node.right;

        node.right = rNode.left;
        rNode.left = node;

        node.height = Math.max(height(node.left), height(node.right)) + 1;
        rNode.height = Math.max(height(rNode.left), height(rNode.right)) + 1;

        return rNode;
    }

    // LR case
    public Node lrRotate(Node node) {
        node.left = leftRotate(node.left);
        return rightRotate(node);
    }

    // RL case
    public Node rlRotate(Node node) {
        node.right = rightRotate(node.right);
        return leftRotate(node);
    }

    //BF 계산
    public int getBalance(Node node) {
        if (node == null) {
            return 0;
        }
        return height(node.left) - height(node.right);
    }
    
    //데이터 추가(BF정보까지 체크)
    public void insert(int key) {
        this.head = insert(this.head, key);

    }

    public Node insert(Node node, int key) {
        if (node == null) {
            return new Node(key, null, null);
        }

        if (key < node.key) {
            node.left = insert(node.left, key);
        } else {
            node.right = insert(node.right, key);
        }

        node.height = Math.max(height(node.left), height(node.right)) + 1;

        int balance = getBalance(node);


        if (balance > 1 && key < node.left.key) {   //LL
            return rightRotate(node);
        }


        if (balance < -1 && key > node.right.key) { //RR
            return leftRotate(node);
        }

        if (balance > 1 && key > node.left.key) {   //LR
            return lrRotate(node);
        }

        if (balance < -1 && key < node.right.key) { //RL
            return rlRotate(node);
        }

        return node;
    }
    
    //데이터 삭제
    public void delete(int key) {
        this.head = delete(this.head, key);
    }

    public Node delete(Node node, int key) {
        if (node == null) {
            return null;
        }

        if (key < node.key) {
            node.left = delete(node.left, key);
        } else if (key > node.key) {
            node.right = delete(node.right, key);
        } else {
            if (node.left == null) {
                return node.right;
            } else if (node.right == null) {
                return node.left;
            } else {
                Node predecessor = node;
                Node successor = node.left;

                while (successor.right != null) {
                    predecessor = successor;
                    successor = successor.right;
                }

                predecessor.right = successor.left;
                node.key = successor.key;
            }
        }

        node.height = Math.max(height(node.left), height(node.right)) + 1;

        int balance = getBalance(node);

        if (balance > 1 && getBalance(node.left) > 0) { //LL
            return rightRotate(node);
        }

        if (balance < -1 && getBalance(node.right) < 0) { //RR
            return leftRotate(node);
        }

        if (balance > 1 && getBalance(node.left) < 0) { //LR
            return lrRotate(node);
        }

        if (balance < -1 && getBalance(node.right) > 0) { //RL
            return rlRotate(node);
        }

        return node;
    }
    
    
}
```

