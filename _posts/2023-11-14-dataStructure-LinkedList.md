---
title:  "[선형 자료구조] 연결 리스트"
category: dataStructure
typora-root-url: ../
toc: true
toc_label: "연결 리스트       (Linked List)"
toc_sticky: true
use_math: true
---

## <br>연결 리스트(Linked List)

- 데이터를 링크로 연결해서 관리하는 자료구조
- 자료의 순서는 정해져 있지만 메모리상 연속성이 보장되지는 않음



### <br>연결 리스트의 장점

- 데이터 공간을 미리 할당할 필요 없음
- 리스트의 길이가 가변적이라 데이터 추가/삭제 용이

### <br>연결 리스트의 단점

- 연결 구조를 위한 별도 데이터 공간 필요
- 연결 정보를 찾는 시간 필요(접근 속도가 상대적으로 느림)
- 데이터 추가,삭제 시 앞뒤 데이터의 연결을 재구성하는 작업 필요



### <br>연결 리스트의 기본 구조

- 노드(Node) : 데이터의 저장 단위로 값과 포인터로 구성

<img src="/images/2023-11-14-algorithm-LinkedList/LinkedList.png" alt="LinkedList" style="zoom:67%;" />



### <br>연결 리스트의 기본 연산

- 삽입
  1. 삽입하고자 하는 new 노드가 after노드를 가리키게 한다.
  2. before 노드의 링크 필드에 after 노드의 주소가 들어 있으므로 before 노드의 링크를 new 노드의 링크로 복사하면 된다.
  3. 그리고 before 의 링크가 new를 가리키게 한다



<img src="/images/2023-11-14-algorithm-LinkedList/insertNode.png" alt="insertNode" style="zoom: 50%;" />



<br>

- 삭제
  1. before 노드의 링크가 after 노드를 가리키도록 변경한다.
  2. after 노드의 주소가 removed 노드의 링크에 있으므로 removed 노드의 링크를 before 노드의 링크로 복사하면 된다.



<img src="/images/2023-11-14-algorithm-LinkedList/deleteNode.png" alt="deleteNode" style="zoom:50%;" />





***

이미지 출처 : <a href = "https://velog.io/@woo_hyun_1/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-4.-%EB%A6%AC%EC%8A%A4%ED%8A%B8">Woohyun-Shin Blog</a>





### <br>연결리스트 구현

#### <br>단순 연결 리스트

```java
//노드 구현
class Node {
    int data;
    Node next;

    Node() {}
    
    Node(int data, Node next) {
        this.data = data;
        this.next = next;
    }
}

class LinkedList {
    Node head;

    LinkedList() {}
    LinkedList(Node node){
        this.head = node;
    }
    
    //연결 리스트 비어있는지 확인
    public boolean isEmpty(){
        if( this.head == null){
            return true;
        }
        return false;
    }
    
    //연결 리스트의 맨 뒤에 데이터 추가
    public void addData(int data) {
        if (this.head == null) {
            this.head = new Node(data, null);
        } else {
            Node cur = this.head;
            while (cur.next != null) {
                cur = cur.next;
            }
            cur.next = new Node(data, null);
        }
    }
    
    /*
     연결리스트에 데이터 추가
     beforeData 가 null인 경우 가장 뒤에 추가
     beforeData 에 값이 있는 경우, 해당 값을 가진 노드 앞에 추가
    */
    public void addData2(int data, Integer beforeData) {
        if (this.head == null) {
            this.head = new Node(data, null);
        } else if (beforeData == null) {
            Node cur = this.head;
            while (cur.next != null) {
                cur = cur.next;
            }
            cur.next = new Node(data, null);
        } else {
            Node cur = this.head;
            Node prev = cur;
            while (cur != null) {
                if (cur.data == beforeData) {
                    if (cur == this.head) {
                        this.head = new Node(data, this.head);
                    } else {
                        prev.next = new Node(data, cur);
                    }
                    break;
                }
                prev = cur;
                cur = cur.next;
            }
        }
    }
    
    //연결 리스트의 데이터 삭제
    public void removeData(int data) {
        if (this.isEmpty()) {
            System.out.println("List is empty");
            return;
        }

        Node cur = this.head;
        Node prev = cur;
        /*
        cur보다 하나 이전단계를 prev가 따라가야한다
        Why? cur  -> 삭제하려는 노드를 지목
             prev -> 이전 노드의 링크를 지목
         */
        while (cur != null) {
            if (cur.data == data) {

                if (cur == this.head) {
                    this.head = cur.next;
                } else {
                    prev.next = cur.next;
                }

                break;
            }
            prev = cur;
            cur = cur.next;
        }
    }
    
    //연결 리스트에서 데이터 찾기
    public void findData(int data) {
        if (this.isEmpty()) {
            System.out.println("List is empty");
            return;
        }

        Node cur = this.head;
        while (cur != null) {
            if (cur.data == data) {
                System.out.println("Data exist!");
                return;
            }
            cur = cur.next;
        }
        System.out.println("Data not found");
    }
    
    //연결 리스트의 모든 데이터 출력
    public void showData() {
        if (this.isEmpty()) {
            System.out.println("List is empty");
            return;
        }

        Node cur = this.head;
        while (cur != null) {
            System.out.print(cur.data + " ");
            cur = cur.next;
        }
        System.out.println();
    }
}
```



#### <br>양방향 연결 리스트

```java
class DoublyLinkedList extends LinkedList {
    NodeBi head;
    NodeBi tail;

    DoublyLinkedList(NodeBi node) {
        this.head = node;
        this.tail = node;
    }

    //연결 리스트 비어있는지 확인
    public boolean isEmpty() {
        if (this.head == null) {
            return true;
        }
        return false;
    }

    //데이터 추가
    public void addData(int data, Integer beforeData) {
        if (this.head == null) {
            this.head = new NodeBi(data, null, null);
            this.tail = this.head;
        } else if (beforeData == null) {
            this.tail.next = new NodeBi(data, null, this.tail);
            this.tail = this.tail.next;
        } else {
            NodeBi cur = this.head;
            NodeBi prev = cur;
            while (cur != null) {
                if (cur.data == beforeData) {
                    if (cur == this.head) {
                        this.head = new NodeBi(data, this.head, null);
                        this.head.next.prev = this.head;
                    } else {
                        prev.next = new NodeBi(data, cur, prev);
                        cur.prev = prev.next;
                    }
                    break;
                }
                prev = cur;
                cur = cur.next;
            }
        }
    }
    //데이터 삭제
    public void removeData(int data) {
        if (this.isEmpty()) {
            System.out.println("List is empty");
            return;
        }

        NodeBi cur = this.head;
        NodeBi prev = cur;

        while (cur != null) {
            if (cur.data == data) {
                if (cur == this.head && cur == this.tail) {
                    this.head = null;
                    this.tail = null;
                } else if (cur == this.head) {
                    this.head = cur.next;
                    this.head.prev = null;
                } else if (cur == this.tail) {
                    this.tail = this.tail.prev;
                    this.tail.next = null;
                } else {
                    prev.next = cur.next;
                    cur.next.prev = prev;
                }
                break;
            }
            prev = cur;
            cur = cur.next;
        }
    }

    public void showData(){
        if(this.isEmpty()){
            System.out.println("List is empty");
            return;
        }

        NodeBi cur = this.head;
        while(cur != null){
            System.out.print(cur.data + " ");
            cur = cur.next;
        }
        System.out.println();
    }

    public void showDataFromTail(){
        if(this.isEmpty()){
            System.out.println("List is empty");
            return;
        }

        NodeBi cur = this.tail;
        while(cur != null){
            System.out.print(cur.data + " ");
            cur= cur.prev;
        }
        System.out.println();
    }
}
```



#### <br>원형 연결 리스트

```java
class CircularLinkedList {
    NodeBi head;
    NodeBi tail;

    CircularLinkedList(NodeBi node) {
        this.head = node;
        this.tail = node;
        node.next = this.head;
        node.prev = this.head;
    }

    public boolean isEmpty() {
        if (this.head == null) {
            return true;
        }
        return false;
    }

    //연결 리스트에 데이터 추가
    public void addData(int data, Integer beforeData) {
        if (this.head == null) {
            NodeBi newNodeBi = new NodeBi(data, null, null);
            this.head = newNodeBi;
            this.tail = newNodeBi;
            newNodeBi.next = newNodeBi;
            newNodeBi.prev = newNodeBi;
        } else if (beforeData == null) { //before_data 가 null 인 경우, 가장 뒤에 추가
            NodeBi newNodeBi = new NodeBi(data, this.head, this.tail);
            this.tail.next = newNodeBi;
            this.head.prev = newNodeBi;
            this.tail = newNodeBi;
        } else { //before_data 에 값이 있는 경우, 해당 값을 가진 노드 앞에 추가
            NodeBi cur = this.head;
            NodeBi prev = cur;
            do {
                if (cur.data == beforeData) {
                    if (cur == this.head) {
                        NodeBi newNodeBi = new NodeBi(data, this.head, this.tail);
                        this.tail.next = newNodeBi;
                        this.head.prev = newNodeBi;
                        this.head = newNodeBi;
                    } else {
                        NodeBi newNodeBi = new NodeBi(data, cur, prev);
                        prev.next = newNodeBi;
                        cur.prev = newNodeBi;
                    }
                    break;
                }
                prev = cur;
                cur = cur.next;
            } while (cur != this.head);
        }
    }

    //연결 리스트에서 특정 값을 가진 노드 삭제
    public void removeData(int data) {
        if (this.isEmpty()) {
            System.out.println("List is empty");
            return;
        }

        NodeBi cur = this.head;
        NodeBi prev = cur;

        while (cur != null) {
            if (cur.data == data) {
                if (cur == this.head && cur == this.tail) {
                    this.head = null;
                    this.tail = null;
                } else if (cur == this.head) {
                    cur.next.prev = this.head.prev;
                    this.head = cur.next;
                    this.tail.next = this.head;
                } else if (cur == this.tail) {
                    prev.next = this.tail.next;
                    this.tail = prev;
                    this.head.prev = this.tail;
                } else {
                    prev.next = cur.next;
                    cur.next.prev = prev;
                }
                break;
            }

            prev = cur;
            cur = cur.next;
        }
    }
    
    public void showData(){
        if(this.isEmpty()){
            System.out.println("List is empty");
            return;
        }
        
        NodeBi cur = this.head;
        while(cur.next != this.head){
            System.out.print(cur.data + " ");
            cur = cur.next;
        }
        System.out.println(cur.data);
    }
}
```

