---
title:  "[비선형 자료구조] 트라이"
category: dataStructure
typora-root-url: ../
toc: true
toc_sticky: true
use_math: true
---

## <br>트라이(Trie)

- 문자열을 저장하고 빠르게 탐색하기 위한 트리 형태의 자료구조


- 정렬된 트리 구조
- 문자열 저장을 위한 메모리가 필요하지만 탐색이 빠름<br>길이가 N인 문자열 탐색의 시간 복잡도 : O(N) 



### 트라이 형태

- 저장되는 문자열 마지막에 Flag 표시

![trie1](/images/2023-11-26-dataStructure-Trie/trie1.png)



### 트라이 삽입 및 삭제

- apple과 app 같이 중복되는 문자 삽입 시 p에 플래그를 적용하여 구분
  - ap(p)l(e) / ():Flag
- 문자열 삭제 시 leaf Node에서 위로 삭제를 진행하다가 Flag를 만나면 종료

![trieInsert](/images/2023-11-26-dataStructure-Trie/trieInsert.png)



### <br>트라이 구현

- Key, Value로 이루어진 노드로 구성
  - key: 알파벳
  - value: 자식노드

```java
import java.util.*;

class Node {
    HashMap<Character, Node> child;
    boolean isTerminal; //Flag

    public Node() {
        this.child = new HashMap<>();
        this.isTerminal = false;
    }
}

class Trie {
    Node root;

    public Trie() {
        this.root = new Node();
    }

    //데이터 추가
    public void insert(String str) {
        Node cur = this.root;

        for (int i = 0; i < str.length(); i++) {
            char c = str.charAt(i);

            // putIfAbsent: c로 시작하는 key가 있으면 추가 아니면 pass
            cur.child.putIfAbsent(c, new Node());
            cur = cur.child.get(c);

            if (i == str.length() - 1) {
                cur.isTerminal = true;
                return;
            }
        }
    }

    //데이터 검색
    public boolean search(String str) {
        Node cur = this.root;

        for (int i = 0; i < str.length(); i++) {
            char c = str.charAt(i);

            if (cur.child.containsKey(c)) {
                cur = cur.child.get(c);
            } else {
                return false;
            }

            if (i == str.length() - 1) {
                if (!cur.isTerminal) {
                    return false;
                }
            }
        }
        return true;
    }

    //데이터 삭제
    public void delete(String str) {
        boolean ret = this.delete(this.root, str, 0);
        if (ret) {
            System.out.println(str + " 삭제 완료");
        } else {
            System.out.println(str + " 단어가 없습니다.");
        }
    }

    public boolean delete(Node node, String str, int idx) {
        char c = str.charAt(idx);

        if (!node.child.containsKey(c)) {
            return false;
        }

        Node cur = node.child.get(c);
        idx++;

        if (idx == str.length()) {
            if (!cur.isTerminal) {
                return false;
            }

            cur.isTerminal = false;
            if (cur.child.isEmpty()) {
                node.child.remove(c);
            }
        } else {
            if (!this.delete(cur, str, idx)) {
                return false;
            }
            if (!cur.isTerminal && cur.child.isEmpty()) {
                node.child.remove(c);
            }
        }
        return true;
    }
}
```



