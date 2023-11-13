---
title:  "(자료구조&알고리즘) - 기초 수학"
category: algorithm
typora-root-url: ../
toc: true
toc_label: "기초 수학"
toc_sticky: true
use_math: true
---

## <br>기초 수학

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

    //생성자
    MySet() {
        this.list = new ArrayList<Integer>();
    }

    //원소 추가(중복 X)
    public void add(int x) {
        for (int item : this.list) {
            if (item == x) {
                return;
            }
        }
        this.list.add(x);
    }

    //교집합
    public MySet retainAll(MySet b) {
        MySet result = new MySet();

        for (int itemA : this.list) {
            for (int itemB : b.list) {
                if (itemA == itemB) {
                    result.add(itemA);
                }
            }
        }
        return result;
    }

    //합집합
    public MySet addAll(MySet b) {
        MySet result = new MySet();

        for (int itemA : this.list) {
            result.add(itemA);
        }

        for (int itemB : b.list) {
            result.add(itemB);
        }
        return result;
    }

    //차집합
    public MySet removeAll(MySet b) {
        MySet result = new MySet();

        for (int itemA : this.list) {
            boolean containFlag = false;

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



## <br>경우의 수

어떤 사건(일)이 일어날 수 있는 경우의 가짓수를 수로 표현한 것입니다.



### <br>합의 법칙

사건 A 또는 사건 B가 일어날 경우의 수입니다.

n(A∪B) = nA + nB - n(A∩B)

- 예제 : 두 개의 주사를 던졌을 때 합이 3 또는 4의 배수일 경우의 수

```java
int[] dice1 = {1, 2, 3, 4, 5, 6};
int[] dice2 = {1, 2, 3, 4, 5, 6};

int nA = 0;
int nB = 0;
int nAandB = 0;

// 기본 풀이 : 3,4,12 배수의 경우의 수를 모두 구한 후 (3의경우의수 + 4의경우의수 - 12경우의수)로 결과 확인
for (int item1 : dice1) {
    for (int item2 : dice2) {
        if ((item1 + item2) % 3 == 0) {
            nA += 1;
        }

        if ((item1 + item2) % 4 == 0) {
            nB += 1;
        }

        if ((item1 + item2) % 12 == 0) {
            nAandB += 1;
        }
    }
}
System.out.println("결과 : " + (nA + nB - nAandB));	//결과 : 20

// HashSet 이용 : Set은 중복값을 포함할 수 없으므로 12경우의수를 계산할 필요가 없다. 
HashSet<ArrayList> allCase = new HashSet<>();
for (int item1 : dice1) {
    for (int item2 : dice2) {
        if ((item1 + item2) % 3 == 0 || (item1 + item2) % 4 == 0) {
            ArrayList list = new ArrayList(Arrays.asList(item1, item2));
            allCase.add(list);
        }
    }
}
System.out.println("Set 결과 : " + allCase.size());	//결과 : 20
```



### <br>곱의 법칙

사건 A와 사건 B가 동시에 일어날 경우의 수입니다.

n(AxB) = n(A) + n(B)

- 예제 : 두 개의 주사위 a, b를 던졌을 때 a는 3의 배수, b는 4의 배수인 경우의 수

```java
int[] dice1 = {1, 2, 3, 4, 5, 6};
int[] dice2 = {1, 2, 3, 4, 5, 6};

int nA = 0;
int nB = 0;

for(int item1 : dice1){
    if(item1 % 3 == 0 ){
        nA++;
    }
}

for(int item2 : dice1){
    if(item2 % 4 == 0 ){
        nB++;
    }
}

System.out.println("결과 : " + nA*nB);
```



### <br>

### 약수

약수는 어떤 수를 나누었을 때 나누어 떨어지게 하는 자연수입니다.

예를 들어 4의 약수는 (1,2,4) 이고 12의 약수는 (1,2,3,4,6,12) 입니다.

```java
public ArrayList getDivisor(int num) {
    ArrayList result = new ArrayList();

    for (int i = 1; i <= (int) num / 2; i++) {
        if (num % i == 0) {
            result.add(i);
        }
    }
    result.add(num);
        
    return result;
}
```



### <br>최대 공약수(GCD : Greatest Common Divisor)

두 수의 약수 중 공통된 약수를 공약수라고 부릅니다. 그 중 가장 큰 공약수를 최대 공약수라고 합니다.

예를 들어 4와 12의 약수 중 공약수는 ( 1,2,4 ) 이고 최대 공약수는 4를 의미합니다.

```java
public int getGCD(int numA, int numB) {
    int gcd = -1;
    
    ArrayList divisorA = this.getDivisor(numA);
    ArrayList divisorB = this.getDivisor(numB);

    for(int itemA : (ArrayList<Integer>) divisorA){
        for (int itemB : (ArrayList<Integer>) divisorB){
            if(itemA == itemB){
                if(itemA > gcd){
                    gcd = itemA;
                }
            }
        }
    }
    return gcd;
}
```



### <br>최소 공배수(LCM : Least Common Multiple)

두 수의 배수들 중 공통된 배수를 공배수라고 부릅니다. 그 중 가장 작은 공배수를 최소 공배수라고 합니다.

예를 들어 2와 3의 배수는 ( 6, 12, 18 ...) 인데 이중 최소 값인 6이 최소 공배수 입니다.

최소 공배수는 `A * B / 최대 공약수(GCD) ` 로 값을 구할 수 있습니다.

```java
public int getLCM(int numA, int numB) {
    int lcm = -1;

    int gcd = this.getGCD(numA, numB);
    if (gcd != -1) {
        lcm = numA * numB / gcd;
    }

    return lcm;
}
```



## <br>순열(permutation)

서로 다른 n개 중에 r 개를 순서와 선택하는 경우의 수입니다.(순서O, 중복X)

$ nPr = \frac {n!}{(n - r)!} = n(n - 1)(n - 2) .... (n - r + 1) $

- 예제1) 5명을 3줄로 세우는 방법

- 예제2) 서로 다른 4명 중 반장, 부반장을 뽑는 방법



```java
// 5!
int n = 5;
int r = 3;
int result = 1;
        
for (int i = n; i >= n - r + 1; i--) {
    result*=i;
}

System.out.println(result);	//결과 : 60
```



### <br>중복 순열

서로 다른 n개 중에 r 개를 순서와 선택하는 경우의 수입니다.(순서O, 중복O)

$ n\Pi r = n^r $

- 예제1) 서로 다른 4개의 수 중 2개를 뽑는 방법(중복 허용)

- 예제2) 후보 2명, 유권자 3명일 때 기명 투표 방법

```java
int n = 4;
int r = 2;
int result = 1;

for (int i = 0; i < r; i++) {
    result*=n;
}

System.out.println(result);	//결과 : 16
//Math이용
System.out.println(Math.pow(n, r));
```





### <br>원 순열

원 모양의 테이블에 n개의 원소를 나열하는 경우의 수 입니다.

$ \frac{n!}{n} = (n-1)! $

- 예제) 원 모양의 테이블에 3명을 앉히는 경우

```java
int n = 3;
int result = 1;

for (int i = 1; i < n; i++) {
    result *= i;
}
System.out.println(result);
```





### <br>팩토리얼(Factorial)

n! 로 나타내며 1부터 n까지의 자연수를 모두 곱하는 것을 의미합니다.

$ n! = n(n-1)(n-2)....1 $


```java
//5!
int n = 5;
int result = 1;

for (int i = 1; i <= n; i++) {
    result*=i;
}
System.out.println(result);	//결과 : 120

//스트림
System.out.println(IntStream.range(2,6).reduce(1,(x,y) -> x*y));
```

