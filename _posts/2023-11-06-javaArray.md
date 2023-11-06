---
title:  "자바(Java) - 배열"
category: java
toc: true
toc_label: "배열(Array)"
toc_sticky: true
typora-root-url: ../

---

## <br>배열(Array)이란?

배열은 같은 타입의 변수들로 이루어진 집합이라고 정의할 수 있습니다.

배열을 구성하는 각각의 값을 배열 요소(element)라고 하며, 배열에서의 위치를 가리키는 숫자를 인덱스(index)라고 합니다.

자바에서 인덱스는 언제나 0부터 시작하며, 0을 포함한 양의 정수만을 가질 수 있습니다.

배열은 선언되는 형식에 따라 1차원 배열, 2차원 배열뿐만 아니라 그 이상의 다차원 배열로도 선언할 수 있습니다.

### <br>

### 일차원 배열

- 문법

```java
int[] array1 = {1,2,3};
char[] array2 = ['a','b','c'];

//array1은 아래와 같이 생성할수도 있다.
int[] array3 = new int[3];
array3[0] = 1;
array3[1] = 2;
array3[2] = 3;
```

- 예제

```java
int[] array1 = new int[3];
int[] array2 = new int[3];

array1[0] = 1;	//인덱스를 이용한 배열의 초기화
array1[1] = 2;
array1[2] = 3;

array2[0] = 4;	// 배열의 길이보다 적은 수의 배열 요소만 초기화

//배열의 출력
System.out.println(array1[0]);	//결과 : 1 (인덱스 값을 지정하여 출력)

//배열 전체값을 출력시 for문을 이용한다.
for(int i = 0; i < array1.length; i++){
    System.out.print(array1[i]+"\t");	// 인덱스를 이용한 배열로의 접근
}
System.out.println();	//줄바꿈

for(int i = 0; i < array2.length; i++){
    System.out.print(array2[i]+"\t");	// 인덱스를 이용한 배열로의 접근
}

//실행 결과
1 2 3
4 0 0
    
//array 를 for-each 문으로 출력
for(int num : array1){
    System.out.print(num+"\t");
}
```

### <br>이차원 배열

다차원 배열 중에서도 현실적으로 이해하기 쉬운 이차원 배열이 가장 많이 사용됩니다.

- 문법

```java
//이차원 배열
int[][] Array = {{1,2,3},{4,5,6}};
int[][] Array2 = new int[2][3];	//2행3열만큼 데이터가 생성된다.

//삼차원 배열
int[][][] Array3 = {{{1,2}{3,4}}{{5,6},{7,8}}};
```

- 예제

```java
int[][] array = {{1,2,3},{4,5,6}};

for (int i = 0; i < array.length; i++) {
    for (int j = 0; j < array[i].length; j++) {
        System.out.print(array[i][j]+"\t");
    }
    System.out.println();
}

System.out.println();	//줄바꿈

for(int[] ints : array){
    for(int anInt : ints ){
        System.out.print(anInt+"\t");
    }
    System.out.println();
}

//실행 결과
1	2	3	
4	5	6	
```

