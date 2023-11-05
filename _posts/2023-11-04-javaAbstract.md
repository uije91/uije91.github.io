---
title:  "자바(Java)-추상 클래스"
category: java
toc: true
toc_label: "추상 클래스"
toc_sticky: true
typora-root-url: ../

---







## 추상 클래스(Abstract Class)

- 하나 이상의 추상 메소드를 포함하는 클래스입니다.
- 반드시 구현해야 하는 부분에 대해 명시적으로 표현해야 합니다.
- 추상클래스 자체는 객체를 생성할 수 없습니다.



### 추상 메소드(Abstract Method)란?

- 자식 클래스에서 반드시 오버라이딩 해야하는 메소드입니다.
- 선언만 하고 구현 내용이 없습니다.

```java
abstract void methodName();
```



### 추상 클래스의 용도

1. 클래스를 설계하는 사람이 여러 사람일 경우, 클래스마다 필드와 메소드가 각각 다른 이름을 가질 수 있습니다다. <br>그렇다면 동일한 기능임에도 불구하고 이름이 다르다 보니 객체마다 사용법이 달라지기 때문에 추상클래스를 생성하여 필드와 메소드명을 통일 시킬 수 있습니다.
2. 공통적인 필드와 메소드를 추상클래스에 선언해두면 클래스를 작성하는데 시간을 절약할 수 있습니다.



- 아래 예제는 스마트폰클래스를 생성할 때 추상클래스를 이용하는 예시를 알아보겠습니다.

```java
//추상클래스로 스마트폰 2G폰 등등 모든 폰의 종류를 포함하는 Phone 클래스를 생성
abstract class Phone {
    //필드
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

//스마트폰이라는 클래스를 만들건데 추상클래스의 메소드를 상속받아서 사용한다.
class SmartPhone extends Phone {
    //생성자
    public SmartPhone(String owner) {
        super(owner);
    }

    //메소드
    public void internetSearch() {
        System.out.println("인터넷 검색을 합니다.");
    }
}

public class PhoneExample {
    public static void main(String[] args) {
        String owner = "의제";
        SmartPhone phone = new SmartPhone(owner);
        phone.turnOn();
        phone.turnOff();
        phone.internetSearch();
    }
}
```



