---
title:  "자바(Java)-변수와 자료형"
category: java
toc: true
toc_label: "변수와 자료형"
toc_sticky: true
---







## 변수(Variable)

데이터를 저장하기 위해 프로그램에 의해 이름을 할당 받은 메모리 공간을 변수라고 합니다. 



### 변수의 이름 규칙

1. 변수의 이름은 문자와 숫자, _(underscore), $로 구성합니다.
2. 숫자로는 시작할 수 없습니다.
3. 대문자와 소문자에 따라 서로 다른 변수로 구분합니다.
4. 변수 이름 사이에 공백은 사용할 수 없습니다.
5. 미리 예약된 이름으로는 사용할 수 없습니다.



### 변수 표기법

1. 카멜 표기법(camelCase)
  - 맨 첫 글자를 제외한 합성어의 첫 글자만 대문자로 표기하는 방식입니다.
  - 주로 변수,메소드명 표기시 사용합니다.
2. 파스칼 표기법(Pascal)
  - 각 문자의 첫 글자를 대문자로 표기하는 방식입니다.
  - 주로 클래스명 표기시 사용합니다.



### 변수의 선언과 초기화

자바에서는 변수를 사용하기 전에 반드시 먼저 변수를 선언하고 초기화해야 합니다.

변수를 선언하는 방법에는 다음과 같이 두 가지 방법이 있습니다.
1. 변수의 선언만 하는 방법
2. 변수의 선언과 동시에 초기화하는 방법

```java
int num;                 // 변수의 선언
System.out.println(num); // 오류 발생
num = 20;                // 변수의 초기화
System.out.println(num); // 20
```





## 자료형(Data Type)

자료형이란 변수가 저장하는 데이터 형식입니다.



### 숫자형(Number)

숫자 형태의 자료형입니다. 정수와 실수형을 표현할 수 있습니다.

```java
//정수형(int : -2147483648~2147483647)
int intNum = 123;
long longNum = 2147483648;

//실수형(float: 4byte / double : 8byte)
float floatNum = 0.23f;
double doubleNum = 1.23;
```



### 문자형(Character)

한 개의 문자 표현에 사용하는 자료형입니다.

```java
char a = 'a';
char z = 'z';
```



### 논리형(Boolean)

참과 거짓을 나타내는 자료형입니다.

```java
boolean isPass = true;
boolean isOk = false;
```



### 문자열(String)

문자들로 이루어진 집합입니다.

```java
String s1 = "Hello World!";
String s2 = "1234";
```



자주 사용하는 문자열 메소드입니다.

```java
//equals : 문자열 비교
String s1="abc";
String s2="abc";
String s3=new String("abc");

s1.equals(s2); //결과 : true
boolean a = s1==s2; //결과 : true
s1.equals(s3); //결과 : true
boolean b = s1==s3; //결과 : false (s3은 s1,s2와 다른객체이다)


//indexOf : 문자열에서 특정문자를 찾기
String s4 = "abc!de";
s4.indexOf("!",0); //결과 : 3 (0번째부터 !가 있는 순서를 찾는다)


//replace : 문자열 치환 replace(기존문자,변경할문자)
s4.replace("abc","cba"); //결과 : cba!de (abc가 cba로 변경) 


//substring : 특정 문자만 출력
s4.substring(0,3) //결과 : abc (0부터 3이전까지의 문자만 출력)

    
//toUpperCase : 모두 대문자로 출력
s4.toUpperCase(); //결과 : ABC!DE

```



### 문자열(StringBuffer)

문자열을 자주 추가하거나 변경할 때 사용하는 자료형입니다.

String과 다르게 객체를 새로 생성하는게 아니기 때문에 문자열 변경에 용이합니다.

```java
StringBuffer sb = new StringBuffer("Hello World!");
```

자주 사용하는 StringBuffer 메소드입니다. 

equals, indexOf, replace, substring 메소드는 String 메소드와 동일한 방법으로 사용됩니다.

```java
//append : 문자열을 추가한다.
sb.append("@#"); //결과 : Hello world!@#
```



### 배열(Array)

많은 수의 데이터를 담을 수 있는 자료형입니다.

```java
int[] array1 = {1,2,3};
char[] array2 = ['a','b','c'];

//array1은 아래와 같이 생성할수도 있다.
int[] array3 = new int[3];
array3[0] = 1;
array3[1] = 2;
array3[2] = 3;
```



### 리스트(List)

배열과 같이 여러 데이터를 담을 수 있는 자료형입니다.

자주 사용하는 리스트(List) 메소드입니다.

```java
ArrayList list = new ArrayList();
//add : 데이터 추가
list.add("array");
list.add("list"); //결과 : [array, list]
//list.add(index,element)
list.add(0,1); //결과 : [1, array, list]


//get : 데이터 불러오기, get(index) : index의 값을 불러온다.
list.get(1); //결과 : array


//size : 리스트의 데이터 갯수 출력
list.size(); //결과 : 3


//remove : 리스트의 데이터를 삭제
list.remove(0);	//결과 : [array, list] (0번 index의 값을 삭제)
list.remove(Integer.valueOf(0)); //데이터 내의 숫자 0의 값을 삭제한다.


//clear : 리스트에 있는 모든데이터를 제거
list.clear();


//sort : 정렬(자료형이 같을때만 사용 가능)
list.sort(Comparator.naturalOrder()); //오름차순 정렬
list.sort(Comparator.reverseOrder()); //내림차순 정렬


//contains : 데이터가 리스트에 들어있는지 체크
list.contains("list"); //결과 : true
list.contains("b");	//결과 : false
```



### 맵(Map)

key와 value형태로 데이터를 저장하는 자료형입니다.

list와 다르게 순서대로 저장되지 않으므로 key값을 이용하여 데이터에 접근합니다.

```java
HashMap map = new HashMap();
map.put("key","value");
```

자주사용하는 맵(Map) 메소드입니다.

```java
//put : 데이터 추가
map.put("a",9000);
map.put("b",10000);
map.put("c",11000);


//get : 데이터 불러오기(value로 표시된다.)
map.get("a"); //결과 : 9000
map.get("z"); //결과 : null


//size : 맵의 데이터 갯수 출력
map.size(); //결과 : 3


//remove : 맵의 데이터를 삭제
map.remove("b"); //결과 : {a=9000, c=11000}


//containsKey : key값이 맵에 있는지 확인
map.containsKey("c"); //결과 : true , 결과가 없을경우 false
```



### 제네릭스(Generics)

변환될 자료형을 개발자가 직접 지정하는 명시적 형변환입니다.

제한적일 수 있지만 안정성을 높여주고 형변환을 줄여줍니다.

```java
//<>안에 String으로 지정하여 해당 자료형만 추가할 수 있게 제한
ArrayList<String> list = new ArrayList<>();
list.add(1);	// String으로 자료형을 정했기때문에 error
list.add("hello");

HashMap<String,Integer> map = new HashMap<>();
map.put(1,2);	//key 값의 자료형이 맞지 않으므로 error
map.put("apple",3);
```



### 타입 변환

기본형 변수중 boolean을 제외한 나머지 변수는 형 변환이 가능합니다.

```java
double doubleNum = 123.456;
int intNum = (int)doubleNum;	//실수형 doubleNum을 정수형으로 변환

String str = "1234";
int num = 1234;
str = Integer.toString(num);	//int를 String 타입으로 변환
num = Integer.parseInt(str);	//String을 int 타입으로 변환
```

- 표현범위가 좁은 범위에서 넓은 범위로 저장될 때, 자동 형 변환이 됩니다.<br>byte < short < int < long < float < double
