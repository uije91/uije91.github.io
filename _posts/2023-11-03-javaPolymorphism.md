---
title:  "자바(Java)-다형성"
category: java
toc: true
toc_label: "다형성"
toc_sticky: true
typora-root-url: ../
---







## 다형성(Polymorphism)

- 나의 객체가 여러 가지 타입을 가질 수 있는 것을 의미한다.
- 부모 클래스 타입의 참조 변수로 자식 클래스 타입의 인스턴스를 참조

```java
class Parent { ... }
class Child extends Parent { ... }
...

Parent p = new Child();  // 허용
Child c = new Parent();  // 오류 발생
```

- 참조 변수가 사용할 수 있는 멤버의 개수가 실제 인스턴스의 멤버 개수보다 같거나 적어야 참조할 수 있다.

```java
class Person {
    public void print() {
        System.out.println("Person.print");
    }
}

class Student extends Person {
    public void print() {
        System.out.println("Student.print");
    }

    public void print2() {
        System.out.println("Student.print2");
    }
}

public class Main {
    public static void main(String[] args) {
        Person p = new Student();
        p.print;	//출력 가능
        p.print2;	//출력 불가능(오버라이딩 된 print까지만 접근 가능)
    }
}
```



### 타입 변환(Casting)

- 서로 상속 관계에 있는 클래스 사이에만 타입변환을 할 수 있다.
- 자식 클래스 타입에서 부모 클래스 타입으로의 타입 변환은 생략할 수 있다.
- 하지만 부모 클래스 타입에서 자식 클래스 타입으로의 타입 변환은 반드시 명시해야 한다.

```java
class Person {...}
class Student extends Person {...}

Person p1 = null;
Student s1 = null;

Person p2 = new Person();
Student s2 = new Student();
//업 캐스팅 : 자식클래스의 객체가 부모클래스의 타입으로 형변환 되는것
Person p3 = new Student();
//다운 캐스팅 : 업 캐스팅된 것을 원상태로 되돌린다. 단, 타입을 명시적으로 지정해야 한다. 
s1 = (Student)p3;
```



### InstanceOf

- 참조 변수가 참조하고 있는 인스턴스의 실제 타입을 확인할 수 있다.

```java
class Parent { }
class Child extends Parent { }
class Brother extends Parent { }

public class Polymorphism {
    public static void main(String[] args) {
        Parent p = new Parent();
        System.out.println(p instanceof Object); // true
        System.out.println(p instanceof Parent); // true
        System.out.println(p instanceof Child);  // false
        System.out.println();

        Parent c = new Child();
        System.out.println(c instanceof Object); // true
        System.out.println(c instanceof Parent); // true
        System.out.println(c instanceof Child);  // true
    }
}
```

