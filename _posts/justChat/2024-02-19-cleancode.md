---
title:  "[북스터디]클린 코드"
category: justChat
typora-root-url: ../
toc: true
toc_sticky: true
---



## <br>01. 클린코드

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

## <br>02. 의미 있는 이름 

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

## <br>03. 함수

### SOLID

> 객체지향 설계의 5가지 원칙

- SRP: 단일 책인 원칙
  - 한 클래스는 하나의 책임만 가져야 한다.
- OCP: 개발-폐쇄 원칙
  - 소프트웨어 요소는 확장에는 열려있으나 변경에는 닫혀 있어야 한다.
- LSP: 리스코프 치환 원칙
  - 서브 타입은 언제나 기반타입으로 교체할 수 있어야 한다.
- ISP: 인터페이스 분리 원칙
  - 자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다.
- DIP: 의존성 역전 원칙
  - 상위 모델은 하위 모델에 의존하면 안된다. 둘 다 추상화에 의존해야한다.
  - 추상화는 세부사항에 의존해서는 안된다. 세부사항은 추상화에 따라 달라진다.

### <br>함수 작성하기

- 함수내 추상화 수준을 동일하게 맞춰서 작게 쪼갠다.
- 함수 인수의 갯수는 0~2개가 적당하다.

```java
// 객체를 인자로 넘기기
Circle makeCircle(double x, double y, double radius);	// X
Circle makeCircle(Point center, double radius);			// O
```

- 부수효과(Side Effect)가 없는 함수
  - 부수효과(Side Effect): 값을 반환하는 함수가 외부 상태를 변경하는 경우

### <br>함수 리팩터링

1. 기능을 구현하는 서투른 함수를 작성한다.
   - 길고, 복잡하고, 중복도 있다.
2. 테스트 코드를 작성한다
   - 함수 내부의 분기와 엣지값마다 빠짐없이 테스트하는 코드를 짠다.
3. 리팩터링 한다
   - 코드를 다듬고, 함수를 쪼개고, 이름을 바꾸고, 중복을 제거한다.



## 4. 주석

### 주석을 최대한 쓰지 말자

- 주석은 나쁜 코드를 보완하지 못한다(코드로도 의도를 표현할 수 있다!)
- 코드의 변화에 따라가지 못하고 주석은 방치된다.(주석은 컴파일 되지 않는다)

```java
// 직원에게 복지 혜택을 받을 자격이 있는지 검사한다.
if ((employee.flag & HOURLY_FLAG) && (employee.age > 65))

// 의미있는 이름을 지으면 해결 된다.
if (employee.isEligibleForFullBenefits())
```

### <br>좋은 주석

- 구현에 대한 정보를 제공한다.
  - 정규식과 같이 보고 이해하기 힘든 포멧에 대한 설명
- 의도와 중요성을 설명한다.
  - 테스트와 같은 곳에서 간단하게 사용할 때

```java
// 스레드를 많이 생성하여 시스템에 영향을 끼쳐 테스트를 만들도록 함
for (int i=0; i < 25000; i++) {
    SomeThread someThread = ThreadBuilder.builder().build();
}

// 유저로부터 입력받을 값을 저장할 때 trim으로 공백제거 필요
String userName = userNameInput.trim();
```

### <br>TODO, FIXME

- TODO: 앞으로 할일, 지금은 해결하지 않지만 나중에 해야할 일을 미리 적어둘 때
- FIXME: 문제가 있지만, 당장 수정할 필요는 없을 때 가능하면 빨리  수정하는게 좋다.

### <br>주석보다 annotation

- annotation: 코드에 대한 메타 데이터
  - 코드의 실행 흐름에 간섭을 주기도 하고, 주석처럼 코드에 대한 정보를 줄 수 있다.
- @Deprecated: 컴파일러가 warning을 발생시킴. IDE에서 사용시 표시
- @NotThreadSafe: Thread Safe하지 않음을 나타냄

### <br>JavaDoc

- Java 코드에서 API 문서를 HTML 형식으로 생성해주는 도구



## <br>05. 형식 맞추기

### 포맷팅이 중요한 이유

- 가독성에 필수적이다.
- 코드를 잘못 해석해 버그를 발생할 여지를 줄인다.

### <br>클린코드 포맷팅

- 적절한 길이 유지(200~500 Line)
  - 일반적으로 큰 파일보다는 작은 파일이 이해하기 쉽다
  - 코드 길이가 200라인을 넘어간다면 여러개의 일을 하고 있을 수 있다.
- 밀접한 개념은 서로 가까이 둔다
  - 행 묶음은 완결된 생각 하나를 표현하기 때문에 개념은 빈 행으로 분리한다.
  - 변수는 사용되는 위치에서 최대한 가까이 선언한다.

### <br>Java Class Declarations

- Class 내부 코드 순서
  1. Static 변수
     - public -> protected -> package -> private순서
  2. instance 변수
     - public -> protected -> package -> private
  3. 생성자
  4. 메서드
     - public 메서드에서 호출되는 private 메서드는 그 아래에 둔다.
       - 가독성 위주로 그룹핑

### <br>Team Coding Convention

- 팀의 코딩 스타일에 관한 약속

- 개발 언어의 컨벤션이 우선이지만 애매한 부분은 팀 컨벤션을 따른다.

  - MySQL Convention
    - 컬럼명은 snake_case로 네이밍 한다.

  - Team Convention
    - enum 타입으로 사용하는 varchar 타입의 경우 컬럼명은 _type으로 끝나도록 네이밍 한다.
