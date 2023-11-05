---
title:  "자바(Java)-예외 처리"
category: java
toc: true
toc_label: "예외 처리"
toc_sticky: true
typora-root-url: ../
---







## 예외 처리

자바 문법에 맞지 않게 코드를 작성하고 컴파일하려고 하면, 자바 컴파일러는 문법 오류(syntax error)가 발생합니다.

또한, 자바 문법에는 맞게 작성되었다 하더라도 프로그램이 실행되면서 예상하지 못한 오류가 발생할 수 있습니다.

이렇게 예상하지 못한 사태가 발생하여 실행 중인 프로그램이 영향을 받는 것을 오류(error)라고 하며 이는 심각한 문제를 초래할 수 있습니다.

이러한 오류(error)는 개발자가 미리 예측할 수 없기에 예외(exception) 처리를 하여 발생할 수 있는 상황을 다른 흐름으로 바꿀 필요가 있습니다.





### 예외 처리 방법

```java
try {
    예외를 처리하길 원하는 실행 코드;
} catch (error1) {
    error1 예외가 발생할 경우에 실행될 코드;
} catch (error2) {
    error2 예외가 발생할 경우에 실행될 코드;
}
...
finally {
    예외 발생 여부와 상관없이 무조건 실행될 코드;
}
```





### 예외 처리 예시

- 0으로 나누기
- 배열 인덱스 초과
- 없는 파일 열기

````java
//0으로 나누기
try{
    int a = 3 / 0;
}catch (ArithmeticException e){
    System.out.println("에러 내용: "+e);
}

//console log
에러 내용: java.lang.ArithmeticException: / by zero

    
//배열 인덱스 초과
int[] b = new int[4];

try{
    b[4] = 1;
}catch (ArrayIndexOutOfBoundsException e){
    System.out.println("에러 내용: "+e);
}

//console log
에러 내용: java.lang.ArrayIndexOutOfBoundsException: Index 4 out of bounds for length 4

        
//없는 파일 열기
try {
    BufferedReader br = new BufferedReader(new FileReader("abc.txt"));
}catch (FileNotFoundException e){
    System.out.println("에러 내용: "+e);
}

//console log
에러 내용: java.io.FileNotFoundException: abc.txt (지정된 파일을 찾을 수 없습니다)
````





### 예외 던지기

#### throw

개발자가 의도적으로 예외를 발생 시킨 후 처리할 때 사용합니다.

예를 들어 은행 업무를 처리하는 프로그램에서 잔고 부족과 같은 예외는 API에 존재하지 않는데 이런 경우에는 개발자가 직접 예외를 정의해야 합니다.
- 다음 예제는 은행 계좌(Account) 클래스를 작성한것입니다. 출금(withdraw) 메소드에서 잔고(balance) 필드와 출금액을 비교하여 잔고가 부족하면 BalanceInsufficientException 을 발생 시키도록 했습니다.

```java
public class Account {
    //예외 클래스 작성 : 예외 클래스 작성시 클래스명 뒤에 Exception을 상속
    public static class BalanceInsufficientException extends Exception{
        public BalanceInsufficientException(String message){
            super(message);
        }
    }
    
    //필드
    private long balance;
    //생성자
    public Account(){}
    //메소드
    public void deposit(int money){
        balance+=money;
    }

    //사용자 정의 예외 발생시키기
    public void withdraw(int money) throws BalanceInsufficientException{
        if(balance<money){
            throw new BalanceInsufficientException("잔고부족: " + (money - balance) + "원이 모자릅니다.");
        }
        balance-=money;
    }

    public static void main(String[] args) {
        Account account = new Account();
        //예금
        account.deposit(1000);
        System.out.println("예금액: "+account.balance);
        //출금
        try{
            account.withdraw(3000);
        }catch (BalanceInsufficientException e){
            System.out.println(e.getMessage());	//사용자 정의 예외 메세지 발생
        }
    }
}
```



#### throws

예외가 발생하면 상위 메소드로 예외를 전가시킬때 사용합니다.

main() 메소드에서는 try-catch로 예외를 최종 처리하는 것이 바람직합니다.

```java
public class ThrowExample {
    public static void findClass() throws ClassNotFoundException{ //throws를 통해 상위 메소드로 예외를 전가
        Class c = Class.forName("java.lang.String2"); //java.lang.String2라는 클래스는 존재하지 않으므로 오류를 발생시킨다.
    }
    
    public static void main(String[] args) {
        //findClass 메소드에서 온 예외를 처리하는 구문을 작성한다.
        try{
            findClass();
        } catch (ClassNotFoundException e) {
            System.out.println("클래스가 존재하지 않습니다.");
        }

    }
}
```

