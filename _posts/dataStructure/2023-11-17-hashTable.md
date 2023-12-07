---
title:  "[선형 자료구조] 해시 테이블"
category: dataStructure
typora-root-url: ../
toc: true
toc_sticky: true
use_math: true
---

## <br>해시 테이블(Hash Table)

- 키(Key), 값(Value)을 대응시켜 저장하는 데이터 구조
  - 키를 통해 해당 데이터에 빠르게 접근 가능

- 해싱(Hashing)
  - 키를 특정 계산식에 넣어 나온 결과를 사용하여 값에 접근하는 과정




### <br>해시 테이블 구조

- 키(Key) : 해시 테이블 접근을 위한 입력 값
- 해시 함수 : 키를 해시 값으로 매핑하는 연산
- 해시 값 : 해시 테이블의 인덱스
- 해시 테이블 : 키-값을 연관시켜 저장하는 데이터 구조



![hash_function](/images/2023-11-17-algorithm-HashTable/hash_function.jpg)



### <br>해시 충돌

- 해시 테이블의 같은 공간에 서로 다른 값을 저장하려는 경우
  - 서로 다른 키의 해시함수를 통한 해시값이 동일한 경우



#### <br>해시 충돌 해결 방법

- 개방 주소법(Open Address)
  - 충돌 시 테이블에서 비어있는 공간의 hash를 찾아 데이터를 저장
  - hash와 value 가 1:1 관계 유지
  - 비어 있는 공간 탐색 방법에 따라 분류(선형 탐사법,제곱 탐사법, 이중 해싱)
  
- 선형 탐사법
  - Linear Probing
  - 빈 공간을 순차적으로 탐사하는 방법 
    - 충돌 발생 지점부터 이후의 빈 공간을 순서대로 탐사
  - 일차 군집화 문제 발생
    - 반복된 충돌 발생 시 해당 지점 주변에 데이터가 물리는 경우 발생
- 제곱 탐사법
  - Quadratic Probing
  - 빈 공간을 n제곱만큼의 간격을 두고 탐사하는 방법
    - 충돌 발생 지점부터 이후의 빈 공간을 n제곱 간격으로 탐사
  - 일차 군집화 문제 일부 보완
  - 이차 군집화 문제 발생 가능성
- 이중 해싱
  - Double Hashing
  - 해싱 함수를 이중으로 사용
    - 해시 함수 1 : 최초 해시를 구할 때 사용
    - 해시 함수 2 : 충돌 발생 시 탐사 이동 간격을 구할 때 사용
  - 선형 탐사, 제곱 탐사에 비해 데이터가 골고루 분포됨

<br>

- 분리 연결법(Separate Chaining)
  - 해시 테이블을 연결 리스트로 구성
  - 충돌 발생 시 테이블 내의 다른 위치를 탐색하는 것이 아닌 연결 리스트를 이용하여 해당 테이블에 데이터 연결



### <br>해시테이블 연습 문제

- 문제1) 주어진 첫 번째 배열을 이용하여 해시 테이블을 초기화 한 후 두 번째 배열이 주어졌을 때 해당 배열 내 데이터가 해시 테이블에 있는지 확인하는 코드를 작성하세요.

```java
public class Solution {
    public void solution(int[] arr1, int[] arr2) {
        Hashtable<Integer, Integer> ht = new Hashtable<>();

        for (int i = 0; i < arr1.length; i++) {
            ht.put(arr1[i], arr1[i]);
        }

        for (int i = 0; i < arr2.length; i++) {
            if (ht.contains(arr2[i])) {
                System.out.println("True");
            } else {
                System.out.println("False");
            }
        }
    }
}
```



<br>

- 문제2) 정수형 배열 nums 와 target 이 주어졌을 때 nums 에서 임의의 두 수를 더해 target 을 구할 수 있는지 확인하는 프로그램을 작성하세요.<br>두 수 의 합으로 target 을 구할 수 있으면 해당 값의 index 를 반환하고 없는 경우 null 을 반환하세요.

```java
public class Solution {
        public int[] solution(int[] numbers, int target) {
        int[] result = new int[2];
        Hashtable<Integer, Integer> ht = new Hashtable<>();

        for (int i = 0; i < numbers.length; i++) {
            if (ht.containsKey(numbers[i])) {
                result[0] = ht.get(numbers[i]);
                result[1] = i;
                return result;
            }
            ht.put(target - numbers[i], i);
        }
        return null;
    }
}
```



### <br>HashTable? , HashMap?

- HashMap 
  - 단일 쓰레드에서 사용하기 좋은 자료구조
  - 동기화를 지원하지 않습니다.
  - Key에 Null 사용이 가능합니다.
  - ConcurrentHashMap을 이용하면 HashTable의 대안으로 사용이 가능합니다.
- HashTable
  - 멀티 쓰레드에서 사용하기 좋은 자료구조지만 HashMap에 비해 느립니다.
  - 동기화를 지원하며 Thread-safe 합니다.
  - Key에 Null 사용이 불가능합니다.

- Thread-safe

  하나의 함수가 한 스레드로부터 호출되어 실행 중일 때, 다른 스레드가 그 함수를 호출하여 동시에 함께 실행되더라도 실행중인 스레드에서의 다른 스레드의 접근을 차단하여 함수의 수행 결과가 올바르게 나오는 것을 의미합니다.
