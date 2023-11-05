---
title:  "자바(Java)-반복문과 제어문"
category: java
toc: true
toc_label: "반복문과 제어문"
toc_sticky: true
typora-root-url: ../
---







## 반복문이란?

반복문이란 프로그램 내에서 똑같은 명령을 일정 횟수만큼 반복하여 수행하도록 제어하는 명령문입니다.



### for문

주어진 횟수만큼 반복하여 실행하는 구조입니다.


```java
for(초기식; 조건식; 증감식){
    반복하여 실행할 내용;
}
```



#### Enhanced for문

for문이 <u>모든 원소를 순회할 경우 사용</u>하며 for-each 문이라는 키워드로도 사용됩니다. 주로 배열의 출력에 사용합니다.

```java
int[] nums = {1,2,3,4,5};

//for문으로 출력
for(int i=0; i<nums.length; i++)
{
    System.out.println(nums[i]);
}

//Enhanced for문으로 출력
for(int n:nums){
    System.out.println(num);
}
```



### while문

조건문이 만족하는 동안 반복하여 실행하는 구조입니다.

while과 do-while 구조가 있으며, do-while문은 내용을 실행 후 조건에 따라서 반복 여부를 결정합니다.


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

일반적으로 반복문에서는 다음 조건식을 검사하기 전까지 루프 안에 있는 모든 명령문을 실행하지만 기타 제어문을 통해 사용자가 루프의 흐름을 직접 제어할 수 있습니다.



### continue문

루프 내에서 사용하며, 해당 루프의 나머지 부분을 건너뛰고 다음 조건식으로 바로 넘어갈 수 있습니다.

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

루프 내에서 사용하며, 조건식의 판단 결과와 상관없이 반복문을 종료하고 싶을 때 사용합니다.

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



### Labeled Loop문

break문과 다르게 지정된 최상단 반복문을 탈출하는 방식입니다.

구구단 예제로 break문과의 차이점을 알아보겠습니다.

break문은 변수가 j인 for문에서만 반복문을 종료하는 것과 다르게 Loop1로 지정된 전체 for문을 종료합니다.

```java
//break문
for (int i = 2; i < 10; i++) {
    for (int j = 1; j < 10 ; j++) {
        if(j==5) break;
        System.out.printf("%02d X %02d : %02d\t",i,j,i*j);
    }
    System.out.println();
}

//결과
02 X 01 : 02	02 X 02 : 04	02 X 03 : 06	02 X 04 : 08	
03 X 01 : 03	03 X 02 : 06	03 X 03 : 09	03 X 04 : 12	
04 X 01 : 04	04 X 02 : 08	04 X 03 : 12	04 X 04 : 16	
05 X 01 : 05	05 X 02 : 10	05 X 03 : 15	05 X 04 : 20	
06 X 01 : 06	06 X 02 : 12	06 X 03 : 18	06 X 04 : 24	
07 X 01 : 07	07 X 02 : 14	07 X 03 : 21	07 X 04 : 28	
08 X 01 : 08	08 X 02 : 16	08 X 03 : 24	08 X 04 : 32	
09 X 01 : 09	09 X 02 : 18	09 X 03 : 27	09 X 04 : 36
    
//Labeled Loop문
Loop1:
for (int i = 2; i < 10; i++) {
    for (int j = 1; j < 10 ; j++) {
        if(j==5) break Loop1;
        System.out.printf("%02d X %02d : %02d\t",i,j,i*j);
    }
    System.out.println();
}

//결과
02 X 01 : 02	02 X 02 : 04	02 X 03 : 06	02 X 04 : 08	
```

