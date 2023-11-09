---
title:  "아스키 코드"
category: SBT
typora-root-url: ../
---

## <br>아스키 코드

아스키 코드(American Standard Code for Information Interchange) 줄여서 ASCII 코드는 ANSI 에서 만든 미국 정보 교환 표준 부호입니다.

아스키는 각 문자를 7비트로 표현하므로 총 2<sup>7</sup> (128)개의 문자를 표현할 수 있습니다.

- 아래는 아스키 코드 표입니다.



<img src="/images/2023-11-09-codingSBT-ASCII/ascii.png" alt="ascii"  />

***



### <br>아스키 코드의 활용

이런 아스키 코드는 문자열 변환에 주로 사용되는데 몇가지 예제를 통해 살펴보겠습니다.

- 예제 1 : 아스키 코드를 이용하여 소문자>대문자 또는 대문자> 소문자로 변환하기

```java
public void solution() {
    Scanner sc = new Scanner(System.in);
    System.out.print("알파벳 입력 : ");
    char input = sc.nextLine().charAt(0);
    int output = 0;
    int step = 'a' - 'A';

    
    if(input >= 'a' && input <= 'z'){
        output = input-step;
    }else if(input >= 'A' && input <= 'Z'){
        output = input+step;
    }else{
        System.out.println("Error! 알파벳을 입력해 주세요.");
    }
    System.out.println((char)output);
}
```

이처럼 문자를 숫자로 변환 후 사이 값을 빼서 문자 변환이 가능합니다.



- 예제 2 : 입력받은 문자(0~9)를 숫자(0~9)로 변환하기

```java
public static void solution() {
    Scanner sc = new Scanner(System.in);
    System.out.print("숫자 입력 : ");
    char input = sc.nextLine().charAt(0);
    int output = 0;

    if(input>='0' && input<='9'){
        output = input-'0';
    }else{
        System.out.println("Error! 1~9까지의 문자를 입력해 주세요.");
    }
    System.out.println(output);
}
```

문자 1은 아스키 코드값 49, 숫자 1은 아스키 코드값 1입니다.
따라서 문자를 숫자로 변환하기 위해서는 문자열 0(아스키 코드값 48)을 빼서 숫자로 변경 합니다.
