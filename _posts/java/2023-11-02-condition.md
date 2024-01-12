---
title:  "자바(Java) - 조건문"
category: java
toc: true
toc_label: "조건문"
toc_sticky: true
typora-root-url: ../
---

# <br>조건문

조건문은 주어진 조건 식의 결과에 따라 별도의 명령을 수행하도록 제어하는 명령문



## <br>IF문

조건에 따라 무엇을 실행할지 판단하는 분기 구조

- 문법


```java
if(조건문1){
    조건문1을 만족할 때 실행할 내용;
}else if(조건문2){
    조건문2을 만족할 때 실행할 내용;
}else{
    그 외 상황에서 실행할 내용;
}
```

## <br>SWITCH문

입력 값에 따라 어떤 case를 실행할지 판단하는 분기 구조

- 문법


```java
switch(입력값){
    case 입력값1:
        실행할 내용;
        break;
    case 입력값2:
        실행할 내용;
        break;
    default:
        실행할 내용;
        break;
}
```

