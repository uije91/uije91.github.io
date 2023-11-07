---
title:  "자바(Java) - 람다식"
category: java
toc: true
toc_label: "람다 표현식(Lambda Expression)"
toc_sticky: true
typora-root-url: ../

---

## <br>람다 표현식(Lambda Expression)

람다식이란 메소드 대신 하나의 식으로 표현한 것입니다.

- 문법

```java
(매개변수목록) -> { 함수몸체 }
```

- 예제 : 더 작은 수를 출력하는 익명 클래스 내용을 람다식으로 구현

```java
interface Compute {
    abstract int min(int x,int y);
    //abstract int max(int x,int y); //인터페이스의 메소드가 2개 이상이면 람다식을 사용할 수 없다.
}

public class LambdaExample {
    public static void main(String[] args) {
        //익명클래스 구현
        Compute compute1 = new Compute() {
            @Override
            public int min(int x, int y) {
                return x<y?x:y;
            }
            //메소드가 2개이상이면 익명클래스는 추가할 수 있다.
            /*
            @Override
            public int max(int x, int y) {
                return x>y?x:y;
            }
            */
        };
        //람다식
        Compute compute2 = (x,y) -> {return x<y?x:y; };


        System.out.println(compute1.min(5,10));
        System.out.println(compute2.min(8,10));
    }

}
```

### <br>람다식의 장점

1. 코드가 간결해집니다.
2. 코드 가독성이 높아집니다.
3. 생산성이 높아집니다.

### <br>람다식의 단점

1. 재사용이 불가능합니다.(익명)
2. 디버깅이 어렵습니다.
3. 재귀 함수(함수 안에 자신의 함수를 다시 호출하는 함수)로는 맞지 않습니다.
