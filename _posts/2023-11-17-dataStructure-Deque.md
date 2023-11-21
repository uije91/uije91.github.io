---
title:  "(선형 자료구조) - 데크"
category: algorithm
typora-root-url: ../
toc: true
toc_label: "데크(Deque)"
toc_sticky: true
use_math: true
---

## <br>데크(Deque)

- 양쪽에서 삽입과 삭제가 모두 가능한 자료구조
  - Deque : Doubly-ended-Queue
  - 스택(Stack)과 큐(Queue)를 합친 형태


<img src="/images/2023-11-17-algorithm-Deque/deq.png" alt="deq" style="zoom:67%;" />

### <br>데크의 종류

- 입력제한 데크(Scroll) : 한쪽의 입력을 제한한 데크
- 출력제한 데크(Shelf) : 한쪽의 출력을 제한한 데크



### <br>데크 기본연산

- 데이터 추가(Enqueue)
  - add() : 값 추가 성공 시 true 반환 , 실패시 IllegalStateException 발생
  - offer() : 값 추가 성공시 true 반환, 실패시 false 반환
  - addFirst() / offerFirst() : 앞(Front) 부분 입력
  - addLast() / offerLast() : 뒤(Rear) 부분 입력

- 데이터 삭제(Dequeue)
  - remove() : 큐가 비어있을경우 NoSuchElementException 발생
  - poll() : 큐가 비어있을경우 null 반환
  - removeFirst() / pollFirst() : 앞(Front) 부분 값  삭제
  - removeLast() / pollLast() : 뒤(Rear) 부분 값 삭제

- 데이터 확인(Front 값)
  - element() : 큐가 비어 있는 경우 NoSuchElementException 에러 발생
  - poll() : 큐가 비어있을 경우 null 반환



### <br>데크 연습문제

- Q1) 데이터 재정렬
  - D_0 -> D_1 -> ... -> D_n-1 -> D_n 순으로 되어 있는 데이터를 D_0 -> D_n -> D_1 -> D_n-1 -> ... 순이 되도록 재정렬 하시오.
  - 입력예시 : [1 - 2 - 3 - 4 - 5] -> [1 -> 5 -> 2 -> 4 -> 3 ]

```java
public class Practice1 {
    public static void reorderData(int[] arr) {
        Deque deque = new ArrayDeque();
        ArrayList result = new ArrayList();

        IntStream.of(arr).forEach(deque::addLast);

        while (!deque.isEmpty()) {
            result.add(deque.removeFirst());

            if (!deque.isEmpty()) {
                result.add(deque.removeLast());
            }
        }
        printData(result.stream().mapToInt(i -> (int) i).toArray());
    }

    public static void printData(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) {
            System.out.print(arr[i] + " -> ");
        }
        System.out.println(arr[arr.length - 1]);
    }
}
```

<br>

- Q2) Palindrome 찾기 : Palindrome 이면 true, 아니면 false 를 반환하세요.
  - Palindrome : 앞으로 읽어도 거꾸로 읽어도 같은 문자열

```java
public class Practice2 {
    public static boolean checkPalindrome(String str) {
        Deque deque = new ArrayDeque();
        boolean isFront = true;
        boolean isPalindrome = true;

        for (String s : str.split("")) {
            deque.addFirst(s);
        }

        while (!deque.isEmpty()) {
            String s1 = (String) deque.pollFirst();
            String s2 = (String) deque.pollLast();

            if (s1 != null && s2 != null && !s1.equals(s2)) {
                isPalindrome = false;
                break;
            }
        }
        return isPalindrome;
    }
}
```



