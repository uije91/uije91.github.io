---
title:  "(자료구조&알고리즘) - 스택"
category: algorithm
typora-root-url: ../
toc: true
toc_label: "스택(Stack)"
toc_sticky: true
use_math: true
---

## <br>스택(Stack)

스택(Stack)은 후입 선출(Last In First Out : LIFO) 원칙을 따르는 선형 자료 구조로 마지막에 들어온 데이터가 먼저 나가는 구조입니다.

스택은 데이터가 입력된 역순으로 처리되어야 할 때 사용되는 자료구조입니다.



### <br>스택의 원리

스택의 원리는 접시 쌓기와 비슷합니다. 

우리가 접시를 쌓을 때 가장 먼저 올린 접시는 아래에 있고 가장 마지막에 올린 접시는 맨 위에 위치합니다.

새로운 접시를 쌓을 때에는 위부터 접시를 올려야 하며 마지막에 올린 접시부터 사용할 수 있습니다.

이처럼 스택도 가장 마지막에 추가한 데이터를 먼저 사용하는 구조입니다.

<img src="/images/2023-11-13-algorithm-stack/stack.webp" alt="stack" style="zoom:80%;" />



### <br>스택의 기본 연산

- Push() : 스택의 맨 위에 요소를 추가합니다.
- Pop() : 스택의 맨 위에서 요소를 제거합니다.
- Peek() : 최상위 요소를 제거하지 않고 값을 가져옵니다.
- IsEmpty() : 스택이 비어 있는지 확인

```java
public Class StackExample(){
    public static void main(String[] args) {
        Stack stack = new Stack();

        //데이터 추가
        stack.push(1);
        stack.push(2);
        stack.push(3);

        //데이터 꺼내기
        System.out.println(stack.pop());

        //스택의 최상단 값 출력(제거X)
        System.out.println(stack.peek());

        //스택 비어 있는지 확인
        System.out.println(stack.isEmpty());
    }
}
```



### <br>스택의 사용 사례

- 웹 브라우저 방문 기록(뒤로 가기)
- 실행 취소(undo)
- 역순 문자열 만들기
- 후위 표기법 계산



 
