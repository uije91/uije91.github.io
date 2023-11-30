---
title:  "[알고리즘] 그리디"
category: algorithm
typora-root-url: ../
toc: true
toc_sticky: true
use_math: true
---

## <br>그리디(Greedy)

- 매 순간 현재 기준으로 최선의 답을 선택해 나가는 기법
  - 빠르게 근사치를 계산할 수 있습니다.
  - 결과적으로 최적해가 아닐 수도 있습니다.




### <br>그리디 알고리즘 예시

- Activity Selection Problem

  - N개의 활동과 각 활동의 시작 / 종료 시간이 주어졌을 때 한 사람이 최대한 많이 할 수 있는 활동의 수 구하기	

  1. 종료 시간 기준으로 정렬
  2. 먼저 종료되는 활동 순, 겹치지 않는 순으로 선택

<img src="/images/2023-11-30-algorithm-greedy/greedy1.png" alt="greedy1" style="zoom:60%;" />

```java
import java.util.ArrayList;
import java.util.Collections;

class Activity {
    String name;
    int start;
    int end;

    public Activity(String name, int start, int end) {
        this.name = name;
        this.start = start;
        this.end = end;
    }
}

public class Main {
    public static void selectActivity(ArrayList<Activity> list) {
        Collections.sort(list, (x1, x2) -> x1.end - x2.end);

        int curTime = 0;
        ArrayList<Activity> result = new ArrayList<>();
        for (Activity item : list) {
            if (curTime <= item.start) {
                curTime = item.end;
                result.add(item);
            }
        }

        for(Activity item : result){
            System.out.print(item.name + " ");
        }
        System.out.println();

    }

    public static void main(String[] args) {
        // Test code
        ArrayList<Activity> list = new ArrayList<>();
        list.add(new Activity("A", 1, 5));
        list.add(new Activity("B", 4, 5));
        list.add(new Activity("C", 2, 3));
        list.add(new Activity("D", 4, 7));
        list.add(new Activity("E", 6, 10));
        selectActivity(list);
    }
}
```



- 거스름돈(동전의 개수 가장 적게)
  - 잔돈 890 , 동전 종류 : 10, 50, 100, 500
  - 큰 동전부터 계산

<img src="/images/2023-11-30-algorithm-greedy/greedy2.png" alt="greedy2" style="zoom:60%;" />

```java
public class Main {
    public static void getChangeCoins(int receivedMoney, int price) {
        final int[] coins = {500, 100, 50, 10, 5, 1};
        HashMap<Integer, Integer> result = new HashMap<>();

        int change = receivedMoney - price;
        int cnt = 0;

        for (int i = 0; i < coins.length; i++) {
            if (change < coins[i]) {
                continue;
            }

            int q = change / coins[i];
            result.put(coins[i], result.getOrDefault(coins[i], 0) + q);

            change %= coins[i];
            cnt += q;
        }

        System.out.println("거스름돈 동전 개수 : " + cnt);
        for (Map.Entry<Integer, Integer> cur : result.entrySet()) {
            System.out.println(cur.getKey() + " : "+cur.getValue());
        }
    }
}
```



### <br>그리디 알고리즘 적용 조건

- 그리디 알고리즘은 빠르지만 최적해를 보장하지는 못함
  - 거스름돈 예제의 경우 [잔돈 890 , 동전 종류 : 10, 50, <u>400</u>, 500] 최적해가 나오지 않을 수도 있음
- 하기 두 가지 조건에 해당하는 경우 적용 가능
  - 탐욕적 선택 특성(Greedy choice property)
    - 지금 선택이 다음 선택에 영양을 주지 않음
  - 최적 부분 구조(Optimal substructure)
    - 전체 문제의 최적해는 부분 문제의 최적해로 이루어짐



### 

