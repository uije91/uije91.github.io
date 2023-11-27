---
title:  "[알고리즘] 정렬"
category: algorithm
typora-root-url: ../
toc: true
toc_sticky: true
use_math: true
---

## <br>정렬(Sorting)

- 특정 값을 기준으로 데이터를 순서대로 배치하는 방법

- 구현 난이도는 쉽지만 속도는 느린 알고리즘
  - 버블 정렬, 삽입 정렬, 선택 정렬

- 구현 난이도는 조금 어렵지만 속도는 빠른 알고리즘
  - 합병 정렬, 힙 정렬, 퀵 정렬, 트리 정렬

- 하이브리드 정렬
  - 팀 정렬, 블록 병합 정렬, 인트로 정렬

- 기타 정렬 알고리즘
  - 기수 정렬, 카운팅 정렬,셸 정렬,보고 정렬


![sorting](/images/2023-11-27-algorithm-sorting/sorting.jpg)





### <br>버블 정렬(Bubble sort)

- 인접한 데이터를 비교하며 자리 바꾸는 방식
- 알고리즘 복잡도: O(n<sup>2</sup>)

<p>
  <img src="/images/2023-11-27-algorithm-sorting/1.png" width="40%">
  <img src="/images/2023-11-27-algorithm-sorting/2.png" width="40%">
</p>

<p>
  <img src="/images/2023-11-27-algorithm-sorting/3.png" width="40%">
  <img src="/images/2023-11-27-algorithm-sorting/4.png" width="40%">
</p>

- 버블 정렬 구현

```java
public class BubbleSort {
    public static void bubbleSort(int[] arr) {
        // case 1
        for (int i = arr.length - 1; i > 0; i--) {
            for (int j = 0; j < i; j++) {
                if (arr[j] > arr[j + 1]) {
                    int tmp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = tmp;
                }
            }
        }
        
        // case 2
        for (int i = 1; i < arr.length - 1; i++) {
            for (int j = 0; j < arr.length - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    int tmp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = tmp;
                }
            }
        }
    }
}
```



### <br>삽입 정렬(Insertion Sort)

- 앞의 데이터를 정렬 해가면서 삽입 위치를 찾아 정렬하는 방식
- 알고리즘 복잡도: O(n<sup>2</sup>)

<p>
  <img src="/images/2023-11-27-algorithm-sorting/Insertion-sort1.png" width="40%">
  <img src="/images/2023-11-27-algorithm-sorting/Insertion-sort2.png" width="40%">
</p>

<p>
  <img src="/images/2023-11-27-algorithm-sorting/Insertion-sort3.png" width="40%">
  <img src="/images/2023-11-27-algorithm-sorting/Insertion-sort4.png" width="40%">
</p>

- 삽입 정렬 구현

```java
public class InsertionSort {
    public static void insertionSort(int[] arr) {
        for (int i = 1; i < arr.length; i++) {
            for (int j = i; j > 0; j--) {
                if (arr[j] < arr[j - 1]) {
                    int tmp = arr[j];
                    arr[j] = arr[j - 1];
                    arr[j - 1] = tmp;
                } else{
                    break;
                }
            }
        }
    }
}
```



### <br>선택 정렬(Selection Sort)

- 최소 또는 최대 값을 찾아서 가장 앞 또는 뒤부터 정렬하는 방식
- 알고리즘 복잡도: O(n<sup>2</sup>)

<p>
  <img src="/images/2023-11-27-algorithm-sorting/Selection-sort1.png" width="45%">
  <img src="/images/2023-11-27-algorithm-sorting/Selection-sort2.png" width="45%">
</p>

<p>
  <img src="/images/2023-11-27-algorithm-sorting/Selection-sort3.png" width="45%">
  <img src="/images/2023-11-27-algorithm-sorting/Selection-sort4.png" width="45%">
</p>

- 선택 정렬 구현

```java
public class SelectionSort {
    public static void selectionSort(int[] arr) {
        // case 1: 최소값을 찾아서 앞쪽의 데이터와 교환
        for (int i = 0; i < arr.length - 1; i++) {
            int min = i;
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[j] < arr[min]) {
                    min = j;
                }
            }
            int tmp = arr[i];
            arr[i] = arr[min];
            arr[min] = tmp;
        }

        // case 2: 최대값을 찾아서 뒤쪽의 데이터와 교환
        for (int i = arr.length - 1; i > 0; i--) {
            int max = i;
            for (int j = i - 1; j >= 0; j--) {
                if (arr[j] > arr[max]) {
                    max = j;
                }
            }
            int tmp = arr[i];
            arr[i] = arr[max];
            arr[max] = tmp;
        }
    }
}
```



### <br>합병 정렬(Merge Sort)

- 배열을 계속 분할하여 길이가 1이 되도록 만들고 인접한 부분끼리 정렬하면서 합병하는 방식
- 알고리즘 복잡도: O(nlogN)

<img src="/images/2023-11-27-algorithm-sorting/merge-sort-1701096130569-10.png" alt="merge-sort" style="zoom:60%;" />

- 합병  정렬 구현

```java
public class MergeSort {
    public static void mergeSort(int[] arr, int[] tmp, int left, int right) {
        if (left < right) {
            int mid = (left + right) / 2;
            mergeSort(arr, tmp, left, mid);
            mergeSort(arr, tmp, mid + 1, right);
            merge(arr, tmp, left, right, mid);
        }
    }

    public static void merge(int[] arr, int[] tmp, int left, int right, int mid) {
        int p = left;
        int q = mid + 1;
        int idx = p;

        while (p <= mid || q <= right) {
            if (p <= mid && q <= right) {
                if (arr[p] <= arr[q]) {
                    tmp[idx++] = arr[p++];
                } else {
                    tmp[idx++] = arr[q++];
                }
            } else if (p <= mid && q > right) {
                tmp[idx++] = arr[p++];
            } else {
                tmp[idx++] = arr[q++];
            }
        }

        for (int i = left; i <= right; i++) {
            arr[i] = tmp[i];
        }
    }
}
```



### <br>힙 정렬(Heap Sort)

- 힙 자료구조 형태의 정렬 방식
- 기존 배열을 최대 힙으로 구조 변경 후 정렬 진행
- 알고리즘 복잡도:O(nlogN)



- 힙 정렬 구현

```java
public class HeapSort {
    public static void heapSort(int[] arr) {
        for (int i = arr.length / 2 - 1; i >= 0; i--) {
            heapify(arr, i, arr.length);
        }

        for (int i = arr.length - 1; i > 0; i--) {
            swap(arr, 0, i);
            heapify(arr, 0, i);
        }
    }

    public static void heapify(int[] arr, int parentIdx, int size) {
        int leftIdx = 2 * parentIdx + 1;
        int rightIdx = 2 * parentIdx + 2;
        int maxIdx = parentIdx;

        if (leftIdx < size && arr[maxIdx] < arr[leftIdx]) {
            maxIdx = leftIdx;
        }

        if (rightIdx < size && arr[maxIdx] < arr[rightIdx]) {
            maxIdx = rightIdx;
        }

        if (parentIdx != maxIdx) {
            swap(arr, maxIdx, parentIdx);
            heapify(arr, maxIdx, size);
        }
    }

    public static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```



### <br>퀵 정렬(Quick Sort)

- 임의의 기준 값(Pivot)을 정하고 그 값을 기준으로 좌우로 분할하며 정렬하는 방식
- 알고리즘 복잡도: O(n<sup>2</sup>)

<img src="/images/2023-11-27-algorithm-sorting/quick-sort1.png" alt="quick-sort1" style="zoom: 45%;" />

<img src="/images/2023-11-27-algorithm-sorting/quick-sort2.png" alt="quick-sort2" style="zoom:45%;" />



- 퀵 정렬 구현

```java
public class QuickSort {
    public static void quickSort(int[] arr, int left, int right) {
        if (left >= right) {
            return;
        }

        int pivot = partition(arr, left, right);
        quickSort(arr, left, pivot - 1);
        quickSort(arr, pivot + 1, right);
    }

    public static int partition(int[] arr, int left, int right) {
        int pivot = arr[left];
        int i = left;
        int j = right;

        while (i < j) {
            while (arr[j] > pivot && i < j) {
                j--;
            }
            while (arr[i] <= pivot && i < j) {
                i++;
            }

            swap(arr, i, j);
        }
        swap(arr,left,i);

        return i;
    }

    public static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```



### <br>트리 정렬(Tree Sort)

- 이진 탐색 트리(BST)를 만들어서 정렬하는 방식
- 알고리즘 복잡도 O(logN)
