---
title:  "자바(Java) - 인터페이스"
category: java
toc: true
toc_label: "인터페이스"
toc_sticky: true
typora-root-url: ../

---

## <br>인터페이스(Interface)

자바에서는 다중 상속을 지원하지 않습니다. 하지만 인터페이스를 이용한다면 다중 상속처럼 사용할 수 있습니다.

인터페이스는 다른 클래스를 작성할 때 기본이 되는 틀을 제공하면서, 다른 클래스 사이의 중간 매개 역할까지 담당하는 일종의 추상 클래스를 의미합니다.

하지만 추상클래스는 생성자, 필드, 일반메소드를 포함할 수 있지만 인터페이스는 <u>추상메소드와 상수만 포함</u> 할 수 있습니다.

- 문법

```java
접근제어자 interface 인터페이스이름 {
    public static final 타입 상수이름 = 값;
    public abstract 반환타입 메소드이름(매개변수);
    ...
}

class 클래스이름 implements 인터페이스이름 { ... }
```

### <br>상속과 인터페이스를 동시 구현

- 예제 : Phone이라는 추상 클래스와 Iphone,Galaxy 2개의 인터페이스를 이용해 아이폰15클래스와 갤럭시 Z Flip5 클래스를 구현

```java
//Phone 추상클래스
abstract class Phone{
    String Owner;

    //생성자
    public Phone(String owner) {
        Owner = owner;
    }

    //메소드
    public void turnOn() {
        System.out.println("폰 전원을 켭니다.");
    }
    public void turnOff() {
        System.out.println("폰 전원을 끕니다.");
    }
}
//인터페이스 IPhone
interface IPhone{
    public abstract void faceId();
    public abstract void applePay();

}
//인터페이스 Galaxy
interface Galaxy{
    public abstract void bioMetrics();
    public abstract void samsungPay();
}

//아이폰15 클래스 구현
class IPhone15 extends Phone implements IPhone{

    public IPhone15(String owner) {
        super(owner);
    }

    @Override
    public void faceId() {
        System.out.println("페이스 아이디로 잠금을 해제합니다.");
    }
    @Override
    public void applePay() {
        System.out.println("애플페이로 결제를 진행합니다.");
    }
}

//갤럭시 Z Flip5 클래스 구현
class GalaxyZFlip5 extends Phone implements Galaxy{
    public GalaxyZFlip5(String owner) {
        super(owner);
    }

    @Override
    public void bioMetrics() {
        System.out.println("지문인식으로 잠금을 해제합니다.");
    }
    @Override
    public void samsungPay() {
        System.out.println("삼성페이로 결제를 진행합니다.");
    }
}
```

