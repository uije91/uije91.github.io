---
title:  "[비선형 자료구조] 우선순위 큐"
category: dataStructure
typora-root-url: ../
toc: true
toc_sticky: true
use_math: true
---

## <br>우선순위 큐(Priority Queue)

- 우선순위가 높은 데이터가 먼저 나옴(≠ FIFO)

  - 모든 데이터에 우선 순위가 있음
  - Dequeue 시, 우선순위가 높은 순으로 나감
  - 우선 순위가 같은 경우는 FIFO

- 우선순위 큐의 enqueue dequeue
  - 최소 힙 및 최대 힙의 삽입 삭제와 같음




### <br>우선순위 큐 구현

- 우선순위 큐를 구현하는 방법 : 배열, 연결 리스트, 힙
- 시간복잡도에 의하여 힙으로 구성

<img src="/images/2023-11-25-dataStructure-PriorityQueue/img.png" alt="img" style="zoom:60%;" />



### <br>우선순위 큐 사용법

```java
class PriorityQueue {
    public static void main(String[] args) {
        // 우선순위: 낮은 숫자 순
        PriorityQueue<Integer> pq = new PriorityQueue<>(); 
        pq.add(5);
        pq.add(7);
        pq.add(3);
        pq.add(1);
        pq.add(9);
        System.out.println(Arrays.toString(pq.toArray())); // [1, 3, 5, 7, 9]

        // 우선순위: 높은 숫자 순
        PriorityQueue<Integer> pq2 = new PriorityQueue<>(Collections.reverseOrder());
        pq2.add(5);
        pq2.add(7);
        pq2.add(3);
        pq2.add(1);
        pq2.add(9);
        System.out.println(Arrays.toString(pq2.toArray())); // [9, 7, 3, 1, 5]
    }
}

// 제네릭스에 클래스를 명시적으로 사용할 경우

// 방법1. 클래스 내에서 설정
class Person implements Comparable<Person> {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(Person o) {
        // 1: 변경안함
        // -1 : 변경

        //새롭게 추가하는 데이터가 더 적을 때 변경(적은 값이 위로 올라감, 오름차순)
        return this.age >= o.age ? 1 : -1;

        //새롭게 추가하는 데이터 가 더 클 때 변경(큰값이 위로 올라감, 내림차순)
        //return this.age >= o.age ? -1 : 1;
    }
}

public class PQExam1 {
     public static void solution(String[] name, int[] age) {
         PriorityQueue<Person> pq = new PriorityQueue<>();

         for (int i = 0; i < name.length; i++) {
             pq.offer(new Person(name[i], age[i]));
         }
     }
}

//방법2. 클래스 초기화시 조건 추가
class Person2 {
    String name;
    String age;
    
    public Person2(String name,int age) {
        this.name = name;
        this.age = age;
    }
}

public class PQExam2 {
     public static void solution(String[] name, int[] age) {
         // 방법2.람다식으로 클래스 초기화시 조건 추가
         PriorityQueue<Person2> pq2 = new PriorityQueue<>
             ((Person2 p1, Person2 p2) -> p1.age >= p2.age ? 1 : -1);
         
         for (int i = 0; i < name.length; i++) {
             pq.offer(new Person(name[i], age[i]));
         }
     }
}
```



### <br>우선순위 큐 연습문제

- Q1) nums 배열에 주어진 정수들 중에서 k 번째로 큰 수를 반환한는 프로그램을 작성하세요.<br>

  입력 예시<br>
  입력: [3, 1, 2, 7, 6, 4] k: 2<br>
  출력: 6<br>

  입력: [1, 3, 7, 4, 2, 8, 9] k: 7<br>
  출력: 1<br>

```java
import java.util.*;

public class Solution {
    // Priority Queue 풀이
    public static int solution1(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int num : nums) {
            pq.offer(num);

            if (pq.size() > k) {
                pq.poll();
            }
        }
        return pq.peek();
    }

    // 정렬 이용 풀이
    public static int solution2(int[] nums, int k) {
        Arrays.sort(nums);
        return nums[nums.length - k];
    }
}
```

- Q2) 돌의 무게 데이터로 이루어진 정수형 stones 배열이 주어졌을 때 다음의 내용에 따라 프로그램을 작성하세요.<br>

  ​	해당 배열로부터 가장 무게가 많이 나가는 돌 두개를 꺼내세요.<br>

  ​	두 개의 돌을 충돌시키는데, 무게가 같으면 둘다 소멸, 무게가 다르면 남은 무게만큼의 돌은 다시 추가합니다.<br>

  ​	이 과정을 반복하며 가장 마지막의 돌의 무게를 출력하세요.<br>	입출력 예시<br>
  ​	입력: [2, 7, 4, 1, 8, 1] / 출력: 1<br>

  ​	입력: [5, 3, 5, 3, 4] / 출력: 2

  ```java
  import java.util.*;
  
  public class Solution {
      public static void solution(int[] stones) {
          PriorityQueue<Integer> pq = new PriorityQueue<>((x, y) -> y - x);
  
          for (int stone : stones) {
              pq.offer(stone);
          }
  
          while (pq.size() > 1) {
              int stone1 = pq.poll();
              int stone2 = pq.poll();
              int diff = Math.abs(stone1 - stone2);
  
              if (diff != 0) {
                  pq.offer(diff);
              }
          }
  
          System.out.println(pq.poll());
      }
  }
  ```

- Q3) nums 배열에 주어진 정수들 중에서 가장 많이 발생한 숫자들 순으로 k 번째 까지 출력하세요.<br>빈도가 같은 경우에는 값이 작은 숫자가 먼저 출력되도록 구현하세요.<br>입출력 예시<br>입력: [1, 1, 1, 2, 2, 3] / k: 2 / 출력: 1, 2<br>입력: [3, 1, 5, 5, 3, 3, 1, 2, 2, 1, 3] / k: 3 / 출력: 3, 1, 2

```java
import java.util.*;

public class Solution {
    // 방법1. 우선순위 큐에서 조건을 지정
    public static void solution1(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        PriorityQueue<Map.Entry<Integer, Integer>> pq =
                new PriorityQueue<Map.Entry<Integer, Integer>>((x, y) -> y.getValue() == x.getValue() ?
                        x.getKey() - y.getKey() : y.getValue() - x.getValue());

        for (Map.Entry<Integer, Integer> item : map.entrySet()) {
            pq.offer(item);
        }

        for (int i = 0; i < k; i++) {
            Map.Entry<Integer, Integer> cur = pq.poll();
            System.out.print(cur.getKey() + " ");
        }
        System.out.println();
    }
    
    
    //방법2. 조건을 생성자로 지정
    class Num implements Comparable<Num> {
        int key;
        int freq;

        public Num(int key, int freq) {
            this.key = key;
            this.freq = freq;
        }

        @Override
        public int compareTo(Num o) {
            if (this.freq == o.freq) {
                return this.key - o.key;
            } else {
                return o.freq - this.freq;
            }
        }
    }

    public static void solution2(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        PriorityQueue<Num> pq = new PriorityQueue<>();
        for (Map.Entry<Integer, Integer> item : map.entrySet()) {
            pq.add(new Solution.new Num(item.getKey(), item.getValue()));
        }

        for (int i = 0; i < k; i++) {
            Num cur = pq.poll();
            System.out.print(cur.key + " ");
        }
        System.out.println();
    }
}
```

- Q4) 문자열 s 가 주어졌을 때, 문자열 내에 동일한 알파벳이 연속적으로 배치되지 않도록 재배치 하세요.<br>재배치가 가능한 경우 재정렬한 문자열을 반환하고 불가능한 경우 null 을 반환하세요.<br>입출력 예시<br>입력: "aabb" / 출력: "abab"<br>입력: "aaca" / 출력: null

```java
import java.util.*;

public class Solution {
    public static String solution(String s) {
        HashMap<String, Integer> map = new HashMap<>();
        for (String item : s.split("")) {
            map.put(item, map.getOrDefault(item, 0) + 1);
        }

        PriorityQueue<Map.Entry<String, Integer>> pq = new PriorityQueue<>
                ((x, y) -> y.getValue() - x.getValue());

        for (Map.Entry<String, Integer> item : map.entrySet()) {
            pq.offer(item);
        }

        StringBuffer sb = new StringBuffer();
        Map.Entry<String, Integer> prev = null;
        while (!pq.isEmpty()) {
            Map.Entry<String, Integer> cur = pq.poll();

            if (prev != null && prev.getValue() > 0) {
                pq.offer(prev);
            }

            sb.append(cur.getKey());
            cur.setValue(cur.getValue() - 1);

            prev = cur;
            if (pq.isEmpty() && prev.getValue() > 0) {
                return null;
            }
        }
        return sb.toString();
    }
}
```

