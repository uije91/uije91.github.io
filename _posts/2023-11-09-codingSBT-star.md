---
title:  "별 찍기"
category: SBT
typora-root-url: ../
---

## <br>별 찍기

for문에 대한 문제라고 하면 가장 먼저 나오는 문제는 별 찍기 문제입니다.

그만큼 기초적인 문제이기도 하지만 막상 하려고 하면 헷갈리는 문제이기 때문에 정리해보겠습니다.



### <br>별 찍기 원리

별 찍기는 이중 for문을 사용합니다..

첫 번째 for문은 열, 두 번째 for문은 행을 생각한다고 생각하면 됩니다.

***

★★★
★★★
★★★

```java
int n = 3;

for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        System.out.print("★");
    }
    System.out.println();
}
System.out.println();
```

***

★

★★

★★★

```java
int n = 3;

for (int i = 0; i < n; i++) {			//0부터 2까지 총 3칸의 열을 생성한다.
    for (int j = 0; j < i+1; j++) {		//i+1(1,2,3)개의 별을 행에 찍는다.
        System.out.print("★");
    }
    System.out.println();
}
System.out.println();
```

***

　　★

　★★

★★★

```java
int n=3;

for (int i = 0; i < n; i++) {			//0부터 2까지 총 3칸의 열을 생성한다.
    for (int j = n-1; j > i; j--) {		//n-1개(2,1,0)의 공백을 생성한다. 
        System.out.print(" ");
    }
    for (int j = 0; j < i+1; j++) {		//그 후 공백옆에 i+1개(1,2,3)의 별을 찍는다. 
        System.out.print("★");
    }
    System.out.println();
}
System.out.println();
```

***

　　★

　★★★

★★★★★

```java
int n = 3;

for (int i = 0; i < n; i++) {			//0부터 2까지 총 3칸의 열을 생성한다.
    for (int j = 0; j < n-i-1; j++) {	//(n-i)-1개(2,1,0)의 공백을 생성한다.
        System.out.print(" ");
    }
    for (int j = 0; j < i*2+1; j++) {	//(i*2)+1개(1,3,5)의 별을 찍는다.
        System.out.print("★");
    }
    System.out.println();
}
System.out.println();
```

***

　　★

　★★★

★★★★★

　★★★

　　★

마지막은 다이아몬드이다.
다이아몬드 같은 경우엔 2개의 영억으로 나누어 생각하면 편하다.

```java
int n = 5;

//상단부
　　★
　★★★
★★★★★

for (int i = 0; i < n/2+1; i++) {
    for (int j = 0; j < n/2-i; j++) {
        System.out.print(" ");
    }
    for (int j = 0; j < i*2+1; j++) {
        System.out.print("★");
    }
    System.out.println();
}
      

//하단부
　★★★
　　★
for (int i = n/2; i > 0; i--) {
    for (int j = 0; j < n/2+1-i ; j++) {
        System.out.print(" ");
    }
    for (int j = 0; j < i*2-1; j++) {
        System.out.print("★");
    }
    System.out.println();
}
System.out.println();
```

