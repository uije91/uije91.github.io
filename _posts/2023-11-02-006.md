---
title:  "자바(Java)-반복문과 제어문"
category: java
toc: true
toc_label: "반복문과 제어문"
toc_sticky: true
typora-root-url: ../
---



## 반복문이란?

반복문이란 프로그램 내에서 똑같은 명령을 일정 횟수만큼 반복하여 수행하도록 제어하는 명령문이다.



### for문

- 주어진 횟수만큼 반복하여 실행하는 구조


```java
for(초기식; 조건식; 증감식){
    반복하여 실행할 내용;
}
```



### for-each문

- for문이 모든 원소를 순회할 경우 for-each문을 통해 간결하게 표현할 수 있다.

```java
//예제
int[] nums = {1,2,3,4,5};

//for문으로 출력
for(int i=0; i<nums.length; i++)
{
    System.out.println(nums[i]);
}

//for-each문으로 출력
for(int n:nums){
    System.out.println(num);
}
```





### while문

- 조건문이 만족하는 동안 반복하여 실행하는 구조

- while과 do-while 구조가 있다


```java
//while문
while(조건식){
    반복하여 실행할 내용;
}

//do-while문
do{
   반복하여 실행할 내용; 
}while(조건식);
```





## 기타 제어문

- 일반적으로 반복문에서는 다음 조건식을 검사하기 전까지 루프 안에 있는 모든 명령문을 실행한다.

  하지만 기타 제어문을 통해 사용자가 루프의 흐름을 직접 제어할 수 있다.



### continue문

- 루프 내에서 사용하며, 해당 루프의 나머지 부분을 건너뛰고 다음 조건식으로 바로 넘어갈 수 있다.
- 아래의 별찍기 예제에서 continue문을 사용하면 어떻게 될까?

```java
//일반 for문
for (int i = 0; i < 5; i++) {
    for (int j = 0; j < i+1; j++) {
        System.out.print("*");
    }
    System.out.println();
}

//일반 for문의 결과
*
**
***
****
*****
    
//continue문 사용
for (int i = 0; i < 5; i++) {
    if(i==3) continue; // i의 값이 3일때 continue문 실행
    for (int j = 0; j < i+1; j++) {
        System.out.print("*");
    }
    System.out.println();
}

//continue문 사용 결과
*
**
***
*****
```



### break문

- 루프 내에서 사용하며, 조건식의 판단 결과와 상관없이 반복문을 종료하고 싶을 때 사용한다.

```java
//일반 for문
for (int i = 0; i < 5; i++) {
    for (int j = 0; j < i+1; j++) {
        System.out.print("*");
    }
    System.out.println();
}

//일반 for문의 결과
*
**
***
****
*****
    
//break문 사용
for (int i = 0; i < 5; i++) {
    if(i==3) break; // i의 값이 3일때 break문 실행
    for (int j = 0; j < i+1; j++) {
        System.out.print("*");
    }
    System.out.println();
}

//break문 사용 결과
*
**
***
```

