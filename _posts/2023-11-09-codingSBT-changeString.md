---
title:  "자료형 뒤집기"
category: SBT
typora-root-url: ../
---

## <br>자료형 뒤집기

입력된 자료형을 거꾸로 뒤집는 문제는 상당히 많이 출제되는 문제입니다.

그 중에서도 크게 두 가지로 분류하면 문자열과 숫자를 뒤집는 문제가 많이 나옵니다.



### <br>문자열 뒤집기

문자열 뒤집기는 여러가지 방법을 사용할 수 있다.

- StringBuilder의 reverse()함수 이용

```java
public void reverseWord(String str){
    StringBuilder answer = new StringBuilder();
    answer.append(str);
   
    answer.reverse();
}
```



- for문을 이용

```java
public void reverseWord(String str){
    for (int i = str.length()-1; i >= 0 ; i--) {
            System.out.print(str.charAt(i));
        }
    System.out.println();
}
```



### <br>정수형 뒤집기

숫자를 뒤집는 방법은 크게 두 가지로 분류할 수 있습니다.

- 숫자를 문자열로 변환 후 문자열을 뒤집어서 숫자로 변환
- 수식을 이용해서 변환



<br>수식을 이용하여 변환하는 방법은 다음과 같습니다.

12345 라는 숫자를 뒤집는 과정을 예로 들어보겠습니다.

- 뒤집을 숫자를 10으로 나누어 나머지를 구합니다. > 12345%10 은 5
- 그 후 12345를 10으로 나눈 후 나머지를 구합니다 > (12345/10) % 10는 4
- 같은 방법으로 진행합니다. <br>(12345/10\*10*...)%10는 3..2..1... 의 과정을 0이 될 때까지 진행합니다.
- 그 후 이어 붙이는데 숫자 값이 출력 될 때 10씩 곱하여 자리수를 늘린 후 더합니다.

```java 
public void reverseNum(int num){
    int numReverse = 0; 		//뒤집은 숫자를 담아줄 변수
    boolean isMinus = false;	//음수 체크 변수
    
    if(num < 0){	//음수체크
        isMinus = true;
        num *= -1;
    }
    
    while(num > 0){
        int r = num%10;	//뒤집을 숫자를 10으로 나눈 나머지를 구한다.
        num /= 10;		//뒤집을 숫자를 10으로 나눈다.
        
        numReverse = (numReverse*10)+r;	//뒤집은 숫자를 담을 곳에 10을 곱하여 자리수를 늘린 후 나머지값을 더한다.
    }
}
```



