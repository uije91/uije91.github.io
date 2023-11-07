---
title:  "자바(Java) - 클래스와 객체"
category: java
toc: true
toc_label: "클래스와 객체"
toc_sticky: true
typora-root-url: ../

---

## <br>클래스와 객체(Class & Object)

자바에서 객체란 실생활에서 우리가 인식할 수 있는 사물이라고 생각하면 됩니다.

이때 객체를 생성하는 틀 또는 설계도와 같은 개념을 클래스(class)라고 합니다.

예를 들어 붕어빵 기계에서 클래스란 붕어빵을 제조하는 틀을 의미하고 이곳에서 생성되는 붕어빵들을 객체라고 합니다.



### <br>인스턴스(Instance)

자바에서 클래스를 사용하기 위해서는 우선 해당 클래스 타입의 객체(object)를 선언해야 합니다.

이렇게 <u>클래스로부터 객체를 선언하는 과정</u>을 클래스의 인스턴스 화라고 합니다.

또한, 이렇게 선언된 해당 클래스 타입의 객체를 인스턴스(instance)라고 합니다.

즉, 인스턴스란 메모리에 할당된 객체를 의미합니다.

### <br>클래스(Class)

클래스는 객체의 상태를 나타내는 필드(field)와 객체의 행동을 나타내는 메소드(method)로 구성됩니다.

즉, 필드(field)란 클래스에 포함된 변수(variable)를 의미합니다.

또한, 메소드(method)란 어떠한 특정 작업을 수행하기 위한 명령문의 집합이라 할 수 있습니다.

- 문법

```java
public class 클래스명{
    //필드(객체 변수)
    //생성자
    //메소드
    //+접근제어자
    //+static
}

클래스명 객체명 = new 클래스명();
```

### <br>메소드(Method)

어떠한 특정 작업을 수행하기 위한 명령문의 집합입니다.

- 문법

```java
접근제어자 반환타입 메소드이름(매개변수목록) { // 선언부
    // 구현부
}
```

### <br>생성자(Constructor)

클래스를 이용해 객체를 생성하면, 해당 객체는 메모리에 즉시 생성됩니다.

생성자에는 규칙이 있는데 클래스명과 생성자명이 같아야하며, 반환타입이 없습니다.

- 문법

```java
public class 클래스명{
    생성자명(){}
}
```

### <br>this,this()

this : 객체 자신을 의미합니다.

this() : 생성자를 의미합니다.

- 예제

```java
class ThisExample{
    //필드
    String name;
    String type;

    //생성자
    public Car2(String name,String type) {
        this.name = name;	//this 는 객체 자신을 의미
        this.type = type;
}
```

### <br>오버로딩(Overloading)

오버로딩이란 하나의 클래스 안에서 같은 이름의 메소드를 여러개 정의하는 것을 의미합니다.

오버로딩은 메소드의 이름이 같아야 하며 매개변수의 개수나 타입이 달라야 합니다.

- 문법

```java
void display(int num1)              
void display(int num1, int num2)    // 매개변수의 개수가 다르다.
void display(int num1, double num2) // 매개변수의 타입이 다르다.
```

### <br>접근 제어자(Access Modifier)

사용자는 언제나 최소한의 정보만으로 프로그램을 손쉽게 사용할 수 있어야 합니다.

그렇기 때문에 접근제어자를 이용하여 정보 은닉을 구체화  할 수 있습니다.

즉 접근 제어자란 클래스의 변수나 메소드에 접근을 제한하는 기능을 제공합니다.

#### <br>접근제어자의 종류

1. private : 해당 클래스에서만 접근 가능
2. default : 해당 패키지 내에서만 접근 가능
3. protected : 해당 패키지 및 상속 받은 클래스에서 접근 가능
4. public : 어디서든 접근 가능

<img src="/images/2023-11-07-javaClass/modifier.png" alt="modifier" style="zoom:80%;" />

### <br>Static

변수나 메소드의 특성을 바꾸는 키워드입니다.

Static은 메모리에 한번만 할당이 됩니다. 즉 Static변수나 메소드는 서로 공유되는 특성을 갖고 있습니다.

그렇기 때문에 객체를 생성하지 않고도 호출이 가능합니다.

- 예제

```java
class StaticExample {
    // 스태틱 변수
    static String name = "abc";
    int number;

    //생성자
    public StaticExample() {
    }

    public StaticExample(String name, int number) {
        this.name = name;
        this.number = number;
    }

    //출력 메소드
    void printInfo() {
        System.out.println("name : " + name);
        System.out.println("number : " + number);
    }

    // 스태틱 메소드
    static void getName() {
        System.out.println("name : " + name);
    }

}

public class Main {
	public static void main(String[] args) {
        StaticExample st = new StaticExample();	
        st.number = 1;	//static으로 지정하지 않은 변수는 객체를 생성해야 사용할 수 있다.
        
        //Static 변수 및 메소드는 객체를 생성하지 않아도 호출이 가능
        StaticExample.name = "Chulsoo";
        StaticExample.getName();
        
        //printInfo 메소드를 출력한다면 name이 static 변수기때문에 st1,st2,st3의 이름은 모두 마지막 설정인 '박효신'으로 출력된다.
        StaticExample st1 = new StaticExample("김범수", 1);
        StaticExample st2 = new StaticExample("나얼", 2);
        StaticExample st3 = new StaticExample("박효신", 3);
        
        st1.printInfo();
        st2.printInfo();
        st3.printInfo();
    }
}
```


