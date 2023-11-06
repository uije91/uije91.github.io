---
title:  "자바(Java) - 내부 클래스"
category: java
toc: true
toc_label: "내부 클래스(Inner Class)"
toc_sticky: true
typora-root-url: ../

---

## <br>내부 클래스(Inner Class)

내부 클래스(inner class)란 하나의 클래스 내부에 선언된 또 다른 클래스를 의미합니다.

- 문법

```java
class Outer{
    ...
        class Inner{
            ...
        }
}
```



### <br>내부 클래스의 특징

1. 내부 클래스에서 외부 클래스의 멤버에 손쉽게 접근할 수 있게 됩니다.

2. 서로 관련 있는 클래스를 논리적으로 묶어서 표현함으로써, 코드의 캡슐화를 증가시킵니다.
3. 외부에서는 내부 클래스에 접근할 수 없으므로, 코드의 복잡성을 줄일 수 있습니다.

### <br>내부 클래스의 종류

#### 인스턴스 클래스(instance class)

문법과 같이 바깥쪽 클래스를 만들어야 사용할 수 있는 클래스입니다.

#### 정적 클래스(static class)

메모리에 상주되기때문에 바깥쪽 클래스가 만들어지지 않아도 사용 가능한 클래스입니다.

#### 지역 클래스(local class)

클래스 안 메소드 안에 클래스가 있는 클래스입니다.

#### 익명 클래스(anonymous class)

익명 클래스(anonymous class)란 다른 내부 클래스와는 달리 이름을 가지지 않는 클래스를 의미합니다.

익명 클래스는 클래스의 선언과 동시에 객체를 생성하므로, 단 하나의 객체만을 생성하는 일회용 클래스입니다.

- 문법

 ```java
 // 익명 클래스는 선언과 동시에 생성하여 참조변수에 대입함.
 클래스이름 참조변수이름 = new 클래스이름(){
     // 메소드의 선언
 };
 ```

### <br>내부 클래스 예제

```java
class Outer{
    //인스턴스 클래스
    public void print(){
        System.out.println("Outer.print");
    }
    class Inner{
        public void innerPrint(){
            Outer.this.print();
        }
    }

    //정적 클래스
    static class InnerStaticClass{
        void innerPrint(){
            //Outer.this.print();   //정적 클래스는 외부로 접근이 안되기 때문에 사용 불가
        }
    }
}

//추상 클래스
abstract class Person{
    public abstract void printInfo();
}

//추상클래스를 상속받는다 : 추상 클래스를 사용하는 첫번째 방법 
class Student extends Person{
    @Override
    public void printInfo() {
        System.out.println("Student.printInfo");
    }
}


public class Main {
    public static void main(String[] args) {
		//외부 클래스
        Outer outer = new Outer();

		//내부 클래스 - 인스턴스
        Outer.Inner inner = new Outer().new Inner();

		//내부 클래스 - 정적 : static이기 떄문에 객체생성은 안하고 클래스 이름으로 접근
        Outer.InnerStaticClass innerStatic = new Outer.InnerStaticClass();

		//익명 클래스 : 추상 클래스를 사용하는 두번째 방법 
        Person p1 = new Person() {
            @Override
            public void printInfo() {
                System.out.println("Main.printInfo");
            }
        };
    }
}
```

