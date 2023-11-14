---
title:  "(선형 자료구조) - 배열"
category: algorithm
typora-root-url: ../
toc: true
toc_label: "배열(Array)"
toc_sticky: true
use_math: true
---

## <br>배열(Array)

- 많은 수의 데이터를 다룰 때 사용하는 자료구조
- 각 데이터를 인덱스와 1:1 대응하도록 구성
- 데이터가 메모리 상에 연속적으로 저장

<img src="/images/2023-11-14-algorithm-Array/array.jpg" alt="array" style="zoom: 67%;" />



### <br>배열의 장점

- 인덱스를 이용하여 **데이터에 빠르게 접근** 가능



### <br>배열의 단점

- 데이터의 추가/삭제가 번거로운 편
- 미리 **최대의 길이를 정해서 생성**해야 함
- 가변 길이 배열은 배열의 크기를 변경할 때마다 새로운 배열을 생성
- 데이터 삭제 시 인덱스를 유지하기 위해 빈 공간 유지



### <br>배열 연습문제

- Q1) 배열 arr 의 모든 데이터에 대해서 짝수 데이터들의 평균과 홀수 데이터들의 평균을 출력하세요.

```java
void Solution(int[] arr){
    float evenSum = 0;
    float oddSum = 0;
    int evenCnt = 0;
    int oddCnt = 0;

    for (int item : arr) {
        if (item % 2 == 0) {
            evenSum += item;
            evenCnt++;
        } else {
            oddSum += item;
            oddCnt++;
        }
    }
    
    System.out.println("짝수 평균: " + evenSum / evenCnt);
    System.out.println("홀수 평균: " + oddSum / oddCnt);
}
```

<br>

- Q2) 배열 arr 에서 target 에 해당하는 값의 인덱스를 출력, 해당 값이 여러 개인 경우 가장 큰 인덱스 출력

``` java
void Solution(int[] arr, int target) {
    int idx = -1;

    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            if (i > idx) {
                idx = i;
            }
        }
    }
    if(idx >= 0) {
        System.out.println(idx);
    }
}
```

<br>

- Q3) 배열 arr 의 데이터 순서를 거꾸로 변경하세요.

```java
void Solution(int[] arr) {
    for (int i = 0; i < arr.length / 2; i++) {
        int tmp = arr[i];
        arr[i] = arr[arr.length - 1 - i];
        arr[arr.length - 1 - i] = tmp;
    }
    for (int num : arr) {
        System.out.print(num);
    }
}
```

<br>

- Q4) 배열 arr 에서 peek 값 모두 출력

```java
void Solution(int[] arr) {
    for (int i = 0; i < arr.length; i++) {
        if (i == 0 && arr[i] > arr[i + 1]) {
            System.out.print(arr[i] + " ");
        } else if (i == arr.length - 1 && arr[i] > arr[i - 1]) {
            System.out.print(arr[i] + " ");
        } else {
            if(arr[i] > arr[i-1] && arr[i] >arr [i+1]){
                System.out.print(arr[i] + " ");
            }
        }
    }
    System.out.println();
}
```

<br>

- Q5) 배열 arr 의 값을 오름차순으로 출력

```java
void Solution(int[] arr) {
    int[] visited = new int[arr.length];
    int visitCnt = 0;
    int minVal = Integer.MAX_VALUE;
    int minIdx = -1;

    while (visitCnt < arr.length) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] < minVal && visited[i] == 0) {
                minVal = arr[i];
                minIdx = i;
            }
        }

        if(minIdx != -1){
            System.out.print(minVal+" ");
            visited[minIdx] = 1;
            visitCnt++;
        }

        minVal=Integer.MAX_VALUE;
        minIdx = -1;
    }
    System.out.println();
}
```

<br>

- Q6) 배열 arr 에서 중복 값을 제거한 새 배열을 만드시오.

```java
void Solution(int[] arr) {
    int[] result = new int[arr.length];
    int cnt = 0;

    for (int i = 0; i < arr.length; i++) {
        boolean isFlag = false;
        for (int j = 0; j < cnt; j++) {
            if(arr[i] == result[j]){
                isFlag = true;
            }
        }

        if(isFlag == false){
            result[cnt++] = arr[i];
        }
    }

    for (int i = 0; i < cnt; i++) {
        System.out.print(result[i]+" ");
    }
    System.out.println();
}
```

<br>

- Q7) 2차원 배열 arr 을 시계방향 90도 회전시킨 결과를 출력하세요.

```java
void Solution(int[][] arr){
    int[][] result = new int[arr[0].length][arr.length];

    for (int i = 0; i < arr.length; i++) {
        for (int j = 0; j < arr[i].length; j++) {
            int r = arr.length-1-i;
            result[j][r] = arr[i][j];
        }
    }
    printArr(arr);
    System.out.println("===========");
    printArr(result);

}

void printArr(int[][] arr){
    for(int[] item1D : arr){
        for(int item : item1D){
            System.out.print(item+ " ");
        }
        System.out.println();
    }
}
```

