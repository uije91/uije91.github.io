---
title:  "자바(Java) - 상속"
category: java
toc: true
toc_label: "상속"
toc_sticky: true
typora-root-url: ../
---

# <br>상속(Inheritance)

- 기존의 클래스에 기능을 추가하거나 재정의하여 새로운 클래스를 정의하는 것을 의미
  - 부모 클래스(상위 클래스, 기초 클래스) : 상속 대상이 되는 기존 클래스

  - 자식 클래스(하위 클래스, 파생 클래스) : 부모 클래스를 상속하는 클래스


- 부모 클래스의 <u>필드</u>와 <u>메소드</u>가 상속되며, 다중 상속은 불가능하다. 
- (private, default) 멤버는 자식 클래스에서 접근이 불가능하다.

```java
class 자식클래스명 extends 부모클래스명 {
    필드;
    메소드;
    ...
}
```



![img_java_inheritance_diagram](/images/2023-11-03-javaInheritance/img_java_inheritance_diagram.png)

## <br>super, super()

super : 부모 클래스로부터 상속받은 필드나 메소드를 자식 클래스에서 참조하는 데 사용하는 참조 변수

super() : 부모 클래스의 생성자를 호출할 때 사용

```java
// 부모 클래스
public class Parent {
    String name;
    String ssn;

    Parent(String name, String ssn) {
        this.name = name;
        this.ssn = ssn;
    }

    Parent() {}
}

// 자식 클래스
class Child extends Parent{
    String name;
    int no;

    public Child(String name, String ssn, int no) {
        //1-1. Parant Class의 name 호출할 경우
        super.name = name;
        this.ssn = ssn;
        this.no = no;
        
        //1-2. Parant Class의 필드 호출
        super(name,ssn);
        this.no = no;
        
        //2. Child Class의 name 호출
        this.name = name;
        this.ssn = ssn;
        this.no = no;
    }
}
```



## <br>오버라이딩(Overriding)

- 부모클래스의 메소드를 자식클래스에서 재정의 할 떄 사용


- 오버라이딩 조건
  1. 메소드의 선언부는 기존 메소드와 완전히 같아야 한다.
  1. 반환 타입은 부모 클래스의 반환 타입으로 타입 변환할 수 있는 타입이라면 변경가능하다.
  1. 부모 클래스의 메소드보다 접근 제어자를 더 좁은 범위로 변경할 수 없다.
  1. 부모 클래스의 메소드보다 더 큰 범위의 예외를 선언할 수 없다.


```java
//부모 클래스
public class Calculator {
    //메소드
    double areaCircle(double r){
        System.out.println("Calculator 객체의 areaCircle() 실행");
        return Math.PI * r * r;
    }
}

//자식 클래스
class Computer extends Calculator{
    @Override //부모 클래스의 메소드 오버라이드
    double areaCircle(double r) {
        System.out.println("Computer 객체의 areaCircle() 실행"); //자식 클래스에서 내용 수정
        return super.areaCircle(r);
    }
}

class ComputerExample{
    public static void main(String[] args) {
        int r = 10;

        //부모 클래스 결과
        Calculator calc = new Calculator();
        System.out.println("원면적 : "+calc.areaCircle(r));

        System.out.println("=================================");

        //자식 클래스 결과
        Computer computer = new Computer();
        System.out.println("원면적 : "+computer.areaCircle(r));
    }
}


//Console log
Calculator 객체의 areaCircle() 실행
원면적 : 314.1592653589793
=================================
Computer 객체의 areaCircle() 실행
Calculator 객체의 areaCircle() 실행
원면적 : 314.1592653589793
```



