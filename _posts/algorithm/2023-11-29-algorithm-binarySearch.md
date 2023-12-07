---
title:  "[알고리즘] 이진 탐색"
category: algorithm
typora-root-url: ../
toc: true
toc_sticky: true
use_math: true
---

## <br>이진 탐색(Binary Search)

- 정렬된 상태의 데이터에서 특정 값을 빠르게 탐색하는 방법
  - 찾고자 하는 값과 데이터 중앙에 있는 값을 비교

  - 찾고자 하는 값과 더 작으면 데이터 왼쪽 부분에서 이진 탐색

  - 찾고자 하는 값이 더 크면 데이터 오른쪽 부분에서 이진 탐색

- 알고리즘 복잡도: O(logN)



### <br>이진 탐색 과정

- 데이터가 우선 <u>정렬</u>된 상태여야 이진 탐색 진행 가능
- 27을 찾는 과정

<img src="/images/2023-11-29-algorithm-binarySearch/binarysearch.png" alt="binarysearch" style="zoom: 50%;" />

- 문법

```java
public class BinarySearch {
    public static void main(String[] args) {
        int[] arr = {1, 2, 5, 10, 20, 30, 40, 50, 60};

        // 데이터가 있는 경우 해당 index 출력
        System.out.println(Arrays.binarySearch(arr,1)); // 0
        System.out.println(Arrays.binarySearch(arr,10)); // 3
        System.out.println(Arrays.binarySearch(arr,30)); // 5

        // 데이터가 없을 경우 삽입할 위치를 -로 변경 후 하나 더 뺀 값으로 출력
        System.out.println(Arrays.binarySearch(arr,3)); // -3
        System.out.println(Arrays.binarySearch(arr,11)); // -5
        System.out.println(Arrays.binarySearch(arr,35)); // -7
    }
}
```

### <br>이진 탐색 구현

```java
public class BinarySearch {
    //반복문 구조
    public static int binarySearch(int arr[], int target) {
        int left = 0;
        int right = arr.length - 1;

        while (left <= right) {
            int mid = (left + right) / 2;

            if (target == arr[mid]) {
                return mid;
            } else if (target < arr[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return -1;
    }
    
    //재귀 호출 구조
    public static int binarySearch2(int[] arr, int target, int left, int right) {
        if (left > right) {
            return -1;
        }

        int mid = (left + right) / 2;

        if (target == arr[mid]) {
            return mid;
        } else if (target < arr[mid]) {
            return binarySearch2(arr, target, left, mid - 1);
        } else {
            return binarySearch2(arr, target, mid + 1, right);
        }
    }
}
```



### <br>연습 문제

- Q1) target 값이 arr 내에 있으면 해당 인덱스 반환, <br>

- 없으면 해당 값이 있을 경우의 위치에 -1을 곱하고 1을 뺀 값을 반환

  <br>[입출력 예시]<br>
  입력 arr: [1, 2, 5, 10, 20, 30, 40, 50, 60]<br>

  target: 30 / 출력: 5<br>
  target: 3 / 출력: -3

```java
public class Practice1 {
    public static int solution(int[] arr, int target) {
        if (arr == null || arr.length == 0) {
            return -1;
        }

        int left = 0;
        int right = arr.length - 1;

        while (left <= right) {
            int mid = (left + right) / 2;
            //오버 플로우시 아래와 같은 방식으로 표현 가능
            mid = left + (right - left) / 2;
            
            if (target == arr[mid]) {
                return mid;
            } else if (target < arr[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return -left - 1;
    }
}
```

- Q2) nums 배열에 원형 상태로 데이터가 정렬되어 있을 때 이진 탐색으로 데이터를 찾는 프로그램을 작성하세요.<br>
  O(log n) 유지 / 배열을 재 정렬하지 않고 풀기

  <br>[입출력 예시]<br>
  arr: [4, 5, 6, 7, 8, 0, 1, 2]<br>

  target: 0 / 출력: 5<br>
  target: 3 / 출력: -1

```java
public class Practice2 {
    public static int solution(int[] arr, int target) {
        if (arr == null || arr.length == 0) {
            return -1;
        }

        int left = 0;
        int right = arr.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (target == arr[mid]) {
                return mid;
            }

            //4, 5, 6, 7, 8, 0, 1, 2
            if (arr[left] < arr[mid]) {
                if (target >= arr[left] && target < arr[mid]) {
                    right = mid - 1;
                } else {
                    left = mid - 1;
                }
            } else {
                //11, 5, 6, 7, 8, 9, 10
                if (target > arr[mid] && target <= arr[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }

        }
        return -1;
    }
}
```

- Q3) row x col 행렬 데이터가 주어졌을 때, target 을 이진 탐색으로 찾는 프로그램을 작성하세요.<br>
  각 행의 데이터는 오름차순으로 정렬 상태

  <br>[입출력 예시]<br>
  행렬: [[1, 3, 7, 8], [10, 11, 15, 20], [21, 30, 35, 60]]<br>
  target: 3 / 출력: true<br>
  target: 13 / 출력: false

```java
public class Practice3 {
    public static boolean solution(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0) {
            return false;
        }

        int left = 0;
        int rows = matrix.length;
        int cols = matrix[0].length;
        int right = rows * cols - 1;

        while (left <= right) {
            int mid = (left + right) / 2;

            if (matrix[mid / cols][mid % cols] == target) {
                return true;
            } else if (matrix[mid / cols][mid % cols] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return false;
    }
}
```

- Q4) 정수형 배열 weights 와 정수 days 가 주어졌다.<br>
  weights 에는 각 상품의 무게들의 정보가 들어있고, days 는 운송 납기일이다.<br>
  상품들은 weights 에 적혀있는 순서대로 실어서 운송해야 하는데,<br>
  days 이내에 운송을 하기 위한 차량의 최소한의 적재량을 계산하는 프로그램을 작성하세요.

  <br>[입출력 예시]<br>
  weights: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]<br>
  days: 5 / 출력: 15<br>
  <br>
  weights: [3, 2, 2, 4, 1, 4]<br>
  days: 3 / 출력: 6

```java
public class Practice4 {
    public static int solution(int[] weights, int days) {
        int left = 0;
        int right = 0;

        // 차량의 최소한의 적재량을 배열로 이용한다.
        for (int w : weights) {
            left = Math.max(left, w);
            right += w;
        }

        while (left <= right) {
            int mid = (left + right) / 2;
            int cnt = 1;
            int cur = 0;

            for (int w : weights) {
                if (cur + w > mid) {
                    cnt += 1;
                    cur = 0;
                }
                cur += w;
            }

            if (cnt > days) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return left;
    }
}
```

- Q5) 정수형 배열 nums 와 정수 m 이 주어졌다.<br>
  nums 에는 양의 정수 값들이 들어 있고, m 은 배열을 부분 배열로 분리할 수 있는 수이다.<br>
  nums 배열을 m 개의 부분 배열로 분리할 때 각 부분 배열의 합중 가장 큰 값이 최소가 되도록 분리했을 때의 합을 출력하세요.

  <br>[입출력 예시]<br>
  nums: [7, 2, 5, 10, 8]<br>
  m: 2 / 출력: 18<br>
  <br>
  nums: [1, 2, 3, 4, 5]<br>
  m: 2 / 출력: 9

```java
public class Practice5 {
    public static int solution(int[] nums, int m) {
        //값의 합을 배열로 만들고 이진 탐색
        int left = 0;
        int right = 0;

        for (int num : nums) {
            left = Math.max(num, left);
            right += num;
        }

        if (m == 1) {
            return right;
        }

        while (left <= right) {
            int mid = left + (right - left) / 2;
            int cnt = 1;
            int total = 0;

            for (int num : nums) {
                total += num;
                if (total > mid) {
                    total = num;
                    cnt++;
                }
            }

            if (cnt <= m) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }
}
```

