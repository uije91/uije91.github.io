---
title:  "(자료구조&알고리즘) - 기초 수학 "
category: algorithm
typora-root-url: ../
toc: true
toc_label: "기초 수학"
toc_sticky: true

---

# <br>기초 수학

본격적으로 자료구조와 알고리즘을 공부하기 전 기초 수학에 대한 정리를 하려고 합니다.

이러한 수학은 실제로 많은 방법으로 사용되는데 그 중 몇 가지를 공부하고 본격적으로 자료구조와 알고리즘 공부로 넘어가겠습니다.



## 집합(Set)

어떤 조건에 의하여 원소(집합을 이루고 있는 각각의 대상)들의 모임을 집합이라고 합니다.

집합의 표현방법은 크게 3가지로 분류합니다.

1. 원소나열법 : 집합에 속하는 원소를 { } 안에 모두 나열하여 나타내는 방법
2. 조건제시법 : 집합에 속하는 원소를 { x\|x에 대한 조건 } 의 꼴로 나타내는 방법
3. 벤 다이어 그램 : 그림을 이용하여 집합을 나타내는 방법

<br>

### <br>교집합(A∩B) 

두 집합이 공통으로 포함하는 원소로 이루어진 집합입니다.

`retainsAll()` 메소드를 사용합니다.

```java
HashSet a = new HashSet(Arrays.asList(1, 2, 3, 4, 5));
HashSet b = new HashSet(Arrays.asList(2, 4, 6, 8, 10));
a.retainAll(b);
System.out.println("교집합: " + a);
```

### <br>합집합(A∪B) 

어느 하나에라도 속하는 원소들을 모두 모은 집합입니다.

`addAll()` 메소드를 사용합니다.

```java
HashSet a = new HashSet(Arrays.asList(1, 2, 3, 4, 5));
HashSet b = new HashSet(Arrays.asList(2, 4, 6, 8, 10));
a.addAll(b);
System.out.println("합집합: "+a);
```

### <br>차집합(A - B)

- A(or B)에만 속하는 원소들의 집합입니다.

- `removeAll()` 메소드를 사용합니다.

```java
HashSet a = new HashSet(Arrays.asList(1, 2, 3, 4, 5));
HashSet b = new HashSet(Arrays.asList(2, 4, 6, 8, 10));
a.removeAll(b);
System.out.println("차집합:" +a);
```

### <br>여집합(A<sup>c</sup>)

- 전체 집합(U) 중 A의 원소가 아닌 것들의 집합입니다.



### Set을 이용하지 않고 구현

```java
class MySet {
    //ArrayList
    ArrayList<Integer> list;
​
    //생성자
    MySet() {
        this.list = new ArrayList<Integer>();
    }
​
    //원소 추가(중복 X)
    public void add(int x) {
        for (int item : this.list) {
            if (item == x) {
                return;
            }
        }
        this.list.add(x);
    }
​
    //교집합
    public MySet retainAll(MySet b) {
        MySet result = new MySet();
​
        for (int itemA : this.list) {
            for (int itemB : b.list) {
                if (itemA == itemB) {
                    result.add(itemA);
                }
            }
        }
        return result;
    }
​
    //합집합
    public MySet addAll(MySet b) {
        MySet result = new MySet();
​
        for (int itemA : this.list) {
            result.add(itemA);
        }
​
        for (int itemB : b.list) {
            result.add(itemB);
        }
        return result;
    }
​
    //차집합
    public MySet removeAll(MySet b) {
        MySet result = new MySet();
​
        for (int itemA : this.list) {
            boolean containFlag = false;
​
            for (int itemB : b.list) {
                if (itemA == itemB) {
                    containFlag = true;
                    break;
                }
            }
            if (!containFlag) {
                result.add(itemA);
            }
        }
        return result;
    }
}
```

