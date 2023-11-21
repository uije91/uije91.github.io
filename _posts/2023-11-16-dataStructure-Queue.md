---
title:  "[선형 자료구조] 큐"
category: dataStructure
typora-root-url: ../
toc: true
toc_sticky: true
use_math: true
---

## <br>큐(Queue)

- 선입선출(First In First Out: FIFO) 자료구조
  - 먼저 들어온 데이터가 먼저 나가는 구조

- 입력 순서대로 데이터 처리가 필요할 때 사용
  - 프린트 출력 대기열, BFS(Breath-First Search) 등




 <img src="/images/2023-11-16-algorithm-Queue/queue.png" alt="queue" style="zoom:60%;" />





### <br>큐의 기본연산

- add() : 데이터 추가(Enqueue)
- poll() : 데이터 꺼내기(Dequeue)
- peek(): 데이터 확인(Front값)

```java
public class QueueExmaple {
    public static void main(String[] args) {
    	Queue queue = new LinkedList();
        
        //데이터 추가
        queue.add(1);
        queue.add(2);
        queue.add(3);
        
        //데이터 꺼내기
        System.out.println(queue.poll());
        
        //데이터 출력(제거X)
        System.out.println(queue.peek());
    }
}
```



### <br>큐 연습문제

- Q1) 1부터 N 까지의 번호로 구성된 N장의 카드가 있다.
  1번 카드가 가장 위에 그리고 N번 카드는 가장 아래의 상태로 카드가 순서대로 쌓여있다.
  아래의 동작을 카드 한 장만 남을 때까지 반복했을 때, 가장 마지막 남는 카드 번호를 출력하시오.
   	1. 가장 위의 카드는 버린다.
   	2. 그 다음 위의 카드는 쌓여 있는 카드의 가장 아래에 다시 넣는다.

```java
public class Solution {
    public static int findLastCard(int N) {
        Queue queue = new LinkedList();

        IntStream.range(1, N + 1).forEach(x -> queue.add(x));
        //System.out.println(queue);

        while (queue.size() > 1) {
            queue.remove();
            int data = (int) queue.remove();
            queue.add(data);
            //System.out.println(queue);
        }

        return (int)queue.remove();
    }
}
```

<br>

- Q2) 요세푸스 문제

  N과 K가 주어졌을 때 (N, K) 요세푸스 순열을 구하시오.
  N과 K는 N >= K 를 만족하는 양의 정수이다.
  1부터 N 번까지 N명이 순서대로 원을 이루어 모여 있다.
  이 모임에서 원을 따라 순서대로 K번째 사람을 제외한다.
  모든 사람이 제외될 때까지 반복하며 이 때, 제외되는 순서가 요세푸스 순열이다.

```java
public class Solution {
    public static ArrayList getJosephusPermutation(int N, int K) {
        Queue queue = new LinkedList();
        ArrayList result = new ArrayList();

        IntStream.range(1, N + 1).forEach(x -> queue.add(x));

        int cnt = 0;
        while (!queue.isEmpty()) {
            int data = (int) queue.remove();
            cnt += 1;

            if (cnt % K == 0) {
                result.add(data);
            } else {
                queue.add(data);
            }
        }
        return result;
    }
}
```

