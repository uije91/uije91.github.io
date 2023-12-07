---
title:  "자바(Java) - 스트림"
category: java
toc: true
toc_label: "스트림(Stream)"
toc_sticky: true
typora-root-url: ../
---

# <br>스트림(Stream)

배열이나 컬렉션 등의 여러 데이터를 다루는 자료형에서 데이터를 하나씩 참조하여 쉽게 처리 가능한 기능을 의미합니다.

스트림 사용을 하게 되면 for문의 사용을 줄여 코드를 간결하게 할 수 있습니다.

스트림은 크게 스트림의 생성,중개 연산, 최종 연산  3가지로 구성할 수 있습니다.

- 문법

```java
데이터소스객체.스트림의생성().중개연산().최종연산();
```

## <br>스트림의 생성

### <br>배열 스트림

배열에 관한 스트림을 생성하기 위해 Arrays 클래스에는 다양한 형태의 stream() 메소드가 클래스 메소드로 정의되어 있습니다.

또한, 기본 타입인 int, long, double 형을 저장할 수 있는 배열에 관한 스트림이 별도로 정의되어 있습니다.

- 예제

```java
String[] arr = new String[]{"a","b","c","d"};
//arr 배열 -> 스트림 생성
Stream arrStream = Arrays.stream(arr);
arrStream.forEach(System.out::println);

// 배열의 특정 부분(1~2번 인덱스만) 만을 이용한 스트림 생성 
Stream arrStream2 = Arrays.stream(arr, 1, 3);
arrStream2.forEach(System.out::println);
```

### <br>컬렉션 스트림

자바에서 제공하는 모든 컬렉션의 최고 상위 조상인 Collection 인터페이스에는 stream() 메소드가 정의되어 있습니다.

따라서 Collection 인터페이스를 구현한 모든 List와 Set 컬렉션 클래스에서도 stream() 메소드로 스트림을 생성할 수 있습니다.

- 예제

```java
ArrayList list = new ArrayList(Arrays.asList(1,2,3));
Stream listStream = list.stream();
listStream.forEach(System.out::println);
```

### <br>가변 매개변수

Stream 클래스의 of() 메소드를 사용하면 가변 매개변수(variable parameter)를 전달받아 스트림을 생성할 수 있습니다.

- 예제

```java
Stream stream = Stream.of(4.2, 2.5, 3.1, 1.9);
stream.forEach(System.out::println);
```

### <br>문자열

Stream 클래스의 builder() 메소드를 이용하여 문자열 스트림을 생성할 수 있습니다.

- 예제

```java
Stream streamBuilder = Stream.builder().add("양파").add(2).add(3.5).build();
streamBuilder.forEach(System.out::println);
```

### <br>지정된 범위의 연속된 정수

지정된 범위의 연속된 정수를 스트림으로 생성하기 위해 IntStream나 LongStream 인터페이스에는 range()와 rangeClosed() 메소드가 정의되어 있습니다.

- 예제

```java
//ragne : 1~4까지의 범위
IntStream intStream1 = IntStream.range(1,5);
intStream1.forEach(System.out::println);

//ragneClosed : 1~5까지의 범위
IntStream intStream2 = IntStream.rangeClosed(1,5);
intStream2.forEach(System.out::println);
```

### <br>람다 표현식

람다 표현식을 매개변수로 전달 받아 해당 람다 표현식에 의해 반환되는 값을 요소로 하는 무한 스트림을 생성하기 위해 Stream 클래스에는 iterate()와 generate() 메소드가 정의되어 있습니다.

- 예제

```java
//generate : generate에 적힌 글자가 limit 만큼 반복 되어 출력
Stream streamGenerate = Stream.generate( () -> "abc").limit(3);
streamGenerate.forEach(System.out::println);

//iterate : 초기값 10 , n *=2 를 limit 만큼 반복
Stream streamIterate = Stream.iterate(10, n -> n*2).limit(3);
streamIterate.forEach(System.out::println);
```



## <br>스트림 중개연산

### <br>스트림 필터링

filter() 메소드는 해당 스트림에서 주어진 조건(predicate)에 맞는 요소만으로 구성된 새로운 스트림을 반환합니다.

또한, distinct() 메소드는 해당 스트림에서 중복된 요소가 제거된 새로운 스트림을 반환합니다.

- 예제

```java
IntStream stream1 = IntStream.range(1,10);
IntStream stream2 = IntStream.of(1,1,2,6,8,10);

//filter : 조건에 맞는 값을 찾음 > 짝수만 골라냄
stream1.filter(n -> n%2==0).forEach(System.out::println);

//distinct : 스트림에서 중복된 요소를 제거함
stream2.distinct().forEach(System.out::println);
```

### <br>스트림 변환

map() 메소드는 해당 스트림의 요소들을 주어진 함수에 인수로 전달하여, 그 반환값들로 이루어진 새로운 스트림을 반환합니다.

filter() 메소드가 조건에 맞는 값을 반환하는 거라면 map() 메소드는 조건에 맞는 값을 변환하여 반환하는 개념입니다.

또한 스트림의 요소가 배열이라면, flatMap() 메소드를 사용하여 각 배열의 각 요소의 반환 값을 하나로 합친 새로운 스트림을 얻을 수 있습니다.

- 예제

```java
//map : 조건에 맞는 값을 변환하여 반환
Stream<String> stream = Stream.of("HTML", "CSS", "JAVA", "JAVASCRIPT");
stream.map(s -> s.length()).forEach(System.out::println);

//flatMap : 배열의 각 요소의 반환 값을 하나로 합친 새로운 스트림을 생성
String[] arr = {"I study hard", "You study JAVA", "I am hungry"};

//" +"는 정규 표현식에서 공백 문자(스페이스)가 하나 이상 있는 패턴을 의미
Stream<String> stream = Arrays.stream(arr);
stream.flatMap(s -> Stream.of(s.split(" +"))).forEach(System.out::println);
```

### <br>스트림 제한

limit() 메소드는 해당 스트림의 첫 번째 요소부터 전달된 개수만큼의 요소만으로 이루어진 새로운 스트림을 반환합니다.

skip() 메소드는 해당 스트림의 첫 번째 요소부터 전달된 개수 만큼의 요소를 제외한 나머지 요소만으로 이루어진 새로운 스트림을 반환합니다.

- 예제

```java
IntStream stream1 = IntStream.range(0, 10);
IntStream stream2 = IntStream.range(0, 10);
IntStream stream3 = IntStream.range(0, 10);

stream1.skip(4).forEach(n -> System.out.print(n + " "));	//결과 : 4 5 6 7 8 9
System.out.println();

stream2.limit(5).forEach(n -> System.out.print(n + " "));	//결과 : 0 1 2 3 4
System.out.println();
```

### <br>스트림 정렬

sorted() 메소드는 해당 스트림을 주어진 비교자(comparator)를 이용하여 정렬합니다.

이때 비교자를 전달하지 않으면 기본적으로 사전 편찬 순(natural order)으로 정렬하게 됩니다.

- 예제

```java
Stream stream = Stream.of(5,1,3,4,2);

//sorted() : 오름차순 정렬
stream.sorted().forEach(System.out::println);

//sorted(Comparator.reverseOrder()) : 내림차순 정렬
stream.sorted(Comparator.reverseOrder()).forEach(System.out::println);
```



## <br>스트림 최종연산

### <br>요소의 출력

forEach() 메소드는 스트림의 각 요소를 소모하여 명시된 동작을 수행합니다.

반환 타입이 void이므로 보통 스트림의 모든 요소를 출력하는 용도로 많이 사용합니다.

- 예제

```java
Stream<String> stream = Stream.of("넷", "둘", "셋", "하나");

//스트림은 일회성이기 때문에 2문장중 1문장만 사용할 수 있다. 
//2문장을 모두 사용하고 싶으면 새로운 변수에 스트림을 저장한 후 사용해야 한다.
stream.forEach(System.out::println);
stream.forEach(s -> System.out.println("숫자 : "+s));
```

### <br>요소의 연산

IntStream이나 DoubleStream과 같은 기본 타입 스트림에는 해당 스트림의 모든 요소에 대해 합과 평균을 구할 수 있는 sum()과 average() 메소드가 각각 정의되어 있습니다.

- 예제 

```java
//sum : 데이터의 합
int sum = IntStream.range(1,5).sum();

//average : 데이터의 합을 Double형으로 출력
double avg = IntStream.range(1,5).average().getAsDouble();
```

### <br>요소의 통계

count() 메소드는 해당 스트림의 요소의 총 개수를 long 타입의 값으로 반환합니다.

또한, max()와 min() 메소드를 사용하면 해당 스트림의 요소 중에서 가장 큰 값과 가장 작은 값을 가지는 요소를 참조하는 객체를 얻을 수 있습니다.

- 예제

```java
//count : 총 개수
long count = IntStream.range(1,5).count();

//min : 최소값
int min = IntStream.range(1,5).min().getAsInt();

//max : 최대값
int max = IntStream.range(1,5).max().getAsInt();
```

### <br>요소의 소모

reduce() 메소드는 첫 번째와 두 번째 요소를 가지고 연산을 수행한 뒤, 그 결과와 세 번째 요소를 가지고 또다시 연산을 수행합니다.

이런 식으로 해당 스트림의 모든 요소를 소모하여 연산을 수행하고, 그 결과를 반환하게 됩니다.

또한, 인수로 초깃값을 전달하면 초깃값과 해당 스트림의 첫 번째 요소와 연산을 시작하며, 그 결과와 두 번째 요소를 가지고 계속해서 연산을 수행하게 됩니다.

- 예제

```java
Stream<Integer> stream = new ArrayList<>(Arrays.asList(1,2,3,4,5)).stream();
int result1 = stream.reduce((x,y)->x + y).get();	//결과 : 순차적으로 1+2+3+4+5 를 해서 15란 값을 출력
int result2 = stream.reduce(20,(x,y) -> x+y);		//결과 : 초기값 20에 순차적으로 +1+2+3+4+5 하여 35 출력
```

