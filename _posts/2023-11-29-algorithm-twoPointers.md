---
title:  "[알고리즘] 투 포인터"
category: algorithm
typora-root-url: ../
toc: true
toc_sticky: true
use_math: true
---

## <br>투 포인터(Two Pointers)

- 배열에서 두 개의 포인터를 사용하여 원하는 결과를 얻는 방법
- 두 개 포인터의 배치 방법
  - 같은 방향에서 시작 : 첫 번째 원소에 둘 다 배치
  - 서로 다른 방향에서 시작 : 첫 번째 원소와 마지막 원소에 배치

- 다중 for문의 복잡도를 좀 더 선형적으로 풀 수 있음



### <br>투 포인터 예시

<img src="/images/2023-11-29-algorithm-twoPointers/tp.webp" alt="tp" style="zoom: 60%;" />



### <br>투 포인터 구현

```java
public class TwoPointers {
    // for문을 이용한 구현
    public static int[] forLoop(int[] arr, int target) {
        int[] result = {-1, -1};

        for (int i = 0; i < arr.length; i++) {
            int sum = arr[i];
            for (int j = i + 1; j < arr.length; j++) {
                if (sum == target) {
                    result[0] = i;
                    result[1] = j - 1;
                    break;
                }
                sum += arr[j];
            }

            if (sum == target) {
                break;
            }
        }

        return result;
    }

    // Two  Pointers를 이용한 구현
    public static int[] twoPointers(int[] arr, int target) {
        int p1 = 0;
        int p2 = 0;
        int sum = 0;
        int[] result = {-1, -1};

        while (true) {
            if (sum > target) {
                sum -= arr[p1++];
            } else if (p2 == arr.length) {
                break;
            } else {
                sum += arr[p2++];
            }

            if (sum == target) {
                result[0] = p1;
                result[1] = p2 - 1;
                break;
            }
        }

        return result;
    }
}
```



### <br>연습 문제

- Q1) a, b, c, d 로 이루어진 알파벳 문자열에 대해서 다음과 같은 규칙으로 문자열을 정리한 후 남은 문자열을 반환하는 프로그램을 작성하세요.<br>
  양쪽의 문자를 비교한 후 같으면 삭제하는데, 연속해서 같은 문자가 등장하면 함께 삭제한다.<br>
  최종적으로 남은 문자열을 반환하세요.<br>

  <br>[입출력 예시]
  <br>입력 s: "ab" / 출력: "ab"
  <br>입력 s: "aaabbaa" / 출력: (없음)

```java
public class Practice1 {
    public static String solution(String s) {
        if (s == null || s.length() == 0) {
            return null;
        }

        int p1 = 0;
        int p2 = s.length() - 1;

        while (p1 < p2 && s.charAt(p1) == s.charAt(p2)) {
            char c = s.charAt(p2);

            while (p1 <= p2 && s.charAt(p1) == c) {
                p1++;
            }

            while (p1 <= p2 && s.charAt(p2) == c) {
                p2--;
            }
        }

        return s.substring(p1, p2 + 1);
    }
}
```

- Q2) nums1 과 nums2 두 배열이 주어졌을 때 두 배열의 공통 원소를 배열로 반환하는 프로그램을 작성하세요.<br>
  결과 배열의 원소에는 중복 값이 없도록 하며 순서는 상관 없다.

  <br>[입출력 예시]
  <br>nums1: [1, 2, 2, 1] / nums2: [2, 2]
  <br>출력: 2

  <br>nums1: [4, 9, 5] / nums2: [9, 4, 9, 8, 4]
  <br>출력: 4, 9 (or 9, 4)

```java
public class Practice2 {
    public static int[] solution(int[] nums1, int[] nums2) {
        HashSet<Integer> set = new HashSet<>();
        Arrays.sort(nums1);
        Arrays.sort(nums2);

        int p1 = 0;
        int p2 = 0;

        while (p1 < nums1.length && p2 < nums2.length) {
            if (nums1[p1] < nums2[p2]) {
                p1++;
            } else if (nums1[p1] > nums2[p2]) {
                p2++;
            } else {
                set.add(nums1[p1]);
                p1++;
                p2++;
            }
        }

        int[] result = new int[set.size()];
        int idx = 0;
        for (Integer n : set) {
            result[idx++] = n;
        }

        return result;
    }
}
```

- Q3) 문자열 s 를 거꾸로 출력하는 프로그램을 작성하세요.<br>
  단, 각 단어의 알파벳 순서는 그대로 출력합니다.<br>
  문장에 공백이 여러개일 시, 단어와 단어 사이 하나의 공백을 제외한 나머지 공백은 제거하세요.

  <br>[입출력 예시]
  <br>문자열 s: "the sky is blue"
  <br>출력: "blue is sky the"

  <br>문자열 s: "  hello      java    "
  <br>출력: "java hello"

```java
public class Practice3 {
    public static String solution(String s) {
        if (s == null) {
            return null;
        }

        if (s.length() < 2) {
            return s;
        }

        s = removeSpaces(s);
        char[] cArr = s.toCharArray();
        reverseString(cArr, 0, s.length() - 1);
        reverseWords(cArr, s.length());

        return new String(cArr);
    }

    public static String removeSpaces(String s) {
        int p1 = 0;
        int p2 = 0;

        char[] cArr = s.toCharArray();
        int len = s.length();

        while (p2 < len) {
            while (p2 < len && cArr[p2] == ' ') {
                p2++;
            }

            while (p2 < len && cArr[p2] != ' ') {
                cArr[p1++] = cArr[p2++];
            }

            while (p2 < len && cArr[p2] == ' ') {
                p2++;
            }

            if (p2 < len) {
                cArr[p1++] = ' ';
            }
        }

        return new String(cArr).substring(0, p1);
    }

    public static void reverseString(char[] cArr, int i, int j) {
        while (i < j) {
            char tmp = cArr[i];
            cArr[i++] = cArr[j];
            cArr[j--] = tmp;
        }
    }

    public static void reverseWords(char[] cArr, int length) {
        int p1 = 0;
        int p2 = 0;

        while (p1 < length) {
            // p1, p2 로 공백 제외 단어 부분 시작, 끝 설정
            while (p1 < p2 || p1 < length && cArr[p1] == ' ') {
                p1++;
            }

            while (p2 < p1 || p2 < length && cArr[p2] != ' ') {
                p2++;
            }

            reverseString(cArr, p1, p2 - 1);
        }
    }
}
```

- Q4) 주어진 nums 배열에서 3 개의 합이 0이 되는 모든 숫자들을 출력하세요.<br>
  중복된 숫자 셋은 제외하고 출력하세요.

  <br>입출력 예시
  <br>nums: [-1, 0, 1, 2, -1, -4]
  <br>출력: [[-1, -1, 2], [-1, 0, 1]]

  <br>nums: [1, -7, 6, 3, 5, 2]
  <br>출력: [[-7, 1, 6], [-7, 2, 5]]

```java
public class Practice4 {
    public static ArrayList<ArrayList<Integer>> solution(int[] nums) {
        Arrays.sort(nums);
        ArrayList<ArrayList<Integer>> result = new ArrayList<>();

        for (int i = 0; i < nums.length - 2; i++) {
            if (i == 0 || i > 0 && nums[i] != nums[i - 1]) {
                int p1 = i + 1;
                int p2 = nums.length - 1;

                // p1+p2+nums[i] = sum
                // p1 + p2 = sum - nums[i]
                int sum = 0 - nums[i];

                while (p1 < p2) {
                    if (nums[p1] + nums[p2] == sum) {
                        result.add(new ArrayList<>(Arrays.asList(nums[i], nums[p1], nums[p2])));

                        //중복된 데이터 거르기
                        while (p1 < p2 && nums[p1] == nums[p1 + 1]) {
                            p1++;
                        }

                        while (p1 < p2 && nums[p2] == nums[p2 - 1]) {
                            p2--;
                        }

                        p1++;
                        p2--;
                    } else if (nums[p1] + nums[p2] < sum) {
                        p1++;
                    } else {
                        p2--;
                    }
                }
            }

        }

        return result;
    }
}
```

