---
title:  "[북스터디]클린 코드"
category: justChat
typora-root-url: ../
toc: true
toc_sticky: true
---



## <br>1. 클린코드

###  나쁜 코드

- 성능이 나쁜 코드
  - 불필요한 연산이 들어가서 개선의 여지가 있는 코드
- 의미가 모호한 코드
  - 이해하기 어려운 코드
  - 네이밍과 그 내용이 다른 코드
- 중복된 코드
  - 비슷한 내용인데 중복되는 코드들은 버그를 낳는다.

### <br> 클린 코드

- 성능이 좋은 코드
- 의미가 명확한 코드(가독성이 좋은 코드)
- 중복이 제거된 코드

## <br>2. 의미 있는 이름 

### 의미 있는 이름 짓기

- 의미가 분명한 이름 짓기

```java
int a;		// X
int count;	// O
```

- 루프 속 i,j,k 사용하지 않기
  - 인덱스 값이 필요하지 않다면 for-each나 lambda 사용

```java
// for-each
for(String message : messages){
    // ...
}

//lambda
messages.stream().forEach(
	message -> //...
)
```

- i, j, k 대신 맥락에 맞는 이름 사용
  - i,j 대신 row,col / width,height 등 사용

- 통일성 있는 단어 사용하기
  - Member / Customer/ User 등 비슷한 의미일 경우 협의 후 한가지만 사용
- 변수명에 타입 넣지 않기
  - String nameString -> name
  - Int itemPriceAmount -> itemPrice
  - Acount[] acountArray -> accounts

### <br>Google Java Naming Guide

- Package: 모두 소문자, 언더바 사용 X
- Class: 대문자로 시작하는 CamelCase
  - 클래스는 명사,명사구
    - Character,  ImmutableList
  - 인터페이스는 명사,명사구,(형용사)
    - List, Readable
  - 테스트 클래스는 Test로 끝나기
    - HashTest, HashIntegrationTest
- Method: 소문자로 시작하는 CamelCase
  - 메서드는 동사, 동사구
    - sendMessage, stop
  - jUnit 테스트에 underscore 사용되기도 함
    - pop_emptyStack

## <br>3. 함수

