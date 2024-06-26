---
title:  "[알고리즘] 백트래킹"
category: algorithm
typora-root-url: ../
toc: true
toc_sticky: true
use_math: true
---

## <br>백트래킹(Backtracking)

- 모든 경우의 수를 탐색하며 최적해를 구하는 과정에서 유망하지 않은 쪽은 더 이상 구하지 않는 방법

  - 유망(Promising): 해가 될 가능성이 있는 경우 유망하다고 함
  - 가지치기(Pruning): 해가 될 가능성이 없는 경우 해당 노드 제외 하는 것
  - 백트래킹(Backtracking): 유망하지 않은 쪽으로 가지 않고 되돌아 오는 것

  

 

### 백트래킹 예시

- N-Queen 문제 
  - N×N 체스판에 N개의 Queen을 배치하여 두 Queen이 서로 공격하지 못하도록 하는 문제
  - 4x4 체스판에 4 Queen 예시

![nq](/images/2023-12-04-algorithm-backtracking/nq.png)

```java
public class NQueen {
    static int n = 4;
    int[] board = new int[n];
    static int cnt;
    
    public static int nQueen(int row) {
        if (row == n) {
            cnt++;
            for (int i = 0; i < n; i++) {
                System.out.print(board[i] + " ");
            }
            System.out.println();
            return cnt;
        }
        
        for (int i = 0; i < n; i++) {
            board[row] = i;

            // promising
            if (isPromising(row)) {
                nQueen(row + 1);
            }

        }

        return cnt;
    }

    public static boolean isPromising(int row) {
        for (int i = 0; i < row; i++) {
            if (board[row] == board[i] || row - i == Math.abs(board[row] - board[i])) {
                return false;
            }
        }
        return true;
    }
}
```



### <br>연습 문제

- Q1) 정수형 n과 m이 주어졌을 때 1 부터 n 까지의 정수 중에서 중복 없이 m개를 고른 수열을 출력하는 프로그램을 작성하세요.

  <br>[입출력 예시]<br>
  n: 3 / m: 2<br>
  출력: [1, 2], [1, 3], [2, 1], [2, 3], [3, 1], [3, 2]

```java
public class Practice1 {
    public static boolean[] visited;
    public static int[] out;

    public static void solution(int n, int m) {
        visited = new boolean[n];
        out = new int[m];
        permutation(n, m, 0);

    }

    public static void permutation(int n, int m, int depth) {
        if (depth == m) {
            System.out.println(Arrays.toString(out));
            return;
        }

        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                visited[i] = true;
                out[depth] = i + 1;
                permutation(n, m, depth + 1);
                visited[i] = false;
            }
        }
    }
}
```

- Q2) 숫자 7193은 7193도 소수이고 719, 71, 7 도 각각 소수이다.<br>
  n 이 주어졌을 때, n 자리 수 중에 위와 같은 소수를 찾는 프로그램을 작성하세요.

  <br>[입출력 예시]<br>
  입력 n: 3<br>
  출력: 233, 239, 293, 311, 313, 317, 373, 379, 593, 599, 719, 733, 739, 797

```java
public class Practice2 {
    public static ArrayList<Integer> result;

    public static ArrayList<Integer> solution(int n) {
        result = new ArrayList<>();

        int[] primeNum = {2, 3, 5, 7};
        for (int i = 0; i < primeNum.length; i++) {
            backTracking(primeNum[i], 1, n);
        }
        return result;
    }

    public static void backTracking(int primeNum, int len, int n) {
        if (len >= n) {
            result.add(primeNum);
            return;
        }

        for (int i = 0; i < 10; i++) {
            if (i % 2 != 0 || i != 5) {
                int primeCandidate = primeNum * 10 + i;
                if (isPrimeNum(primeCandidate)) {
                    backTracking(primeCandidate, len + 1, n);
                }
            }
        }

    }

    public static boolean isPrimeNum(int num) {
        for (int i = 2; i < num / 2; i++) {
            if (num % i == 0) {
                return false;
            }
        }
        return true;
    }
}
```

- Q3) sols 배열에 5지 선다 문제의 정답들이 적혀있다.<br>
  3번 연속 해서 같은 정답이 있는 경우가 없다는 것을 알아낸 후 문제를 찍어서 푼다고 할 때, 5점 이상을 받을 경우의 수를 출력하세요.<br>
  문제는 총 10문제이며 각 문제당 1점이다.

  <br>[입출력 예시]<br>
  sols: [1, 2, 3, 4, 5, 1, 2, 3, 4, 5]<br>
  결과: 261622

```java
public class Practice3 {
    final static int numOfProblems = 10;
    static int cnt;

    public static void solution(int[] sols) {
        if (sols == null || sols.length != numOfProblems) {
            return;
        }

        cnt = 0;
        int[] submit = new int[numOfProblems];
        backTracking(sols, submit, 0, 0);
        System.out.println(cnt);

    }

    public static void backTracking(int[] sols, int[] submit, int correctCnt, int idx) {
        // 총 문항수 - 현재 풀고있는 문제수 + 현재까지 맞은 수
        if (numOfProblems - idx + correctCnt < 5) {
            return;
        }

        if (idx == numOfProblems) {
            if (correctCnt >= 5) {
                cnt += 1;
            }
        } else {
            //같은 값을 두번 썼을 때 다음값을 체크할 변수
            int towInRow = 0;
            if (idx >= 2) {
                if (submit[idx - 1] == submit[idx - 2]) {
                    towInRow = submit[idx - 1];
                }
            }

            for (int i = 1; i <= 5; i++) {
                if (i == towInRow) {
                    continue;
                }

                submit[idx] = i;
                if (sols[idx] == i) {
                    backTracking(sols, submit, correctCnt + 1, idx + 1);
                } else {
                    backTracking(sols, submit, correctCnt, idx + 1);
                }
                submit[idx] = 0;
            }
        }
    }
}
```

- Q4) 2차원 배열 board 가 주어졌다.<br>해당 배열 데이터에는 'o', '#', '.' 의 정보가 기입되어 있다.<br>'o': 동전을 의미<br>'#': 벽을 의미<br>'.': 빈칸을 의미<br><br>동전은 항상 두개가 주어진다.<br>두 동전이 함께 이동하다가 하나가 보드에서 떨어지는 경우의 최소 이동 횟수를 출력하는 프로그램을 작성하세요.<br>단, 이동 규칙은 다음과 같다.
  1. 동전은 좌, 우, 위, 아래로 이동 가능하며 같은 방향으로 함께 이동
  2. 빈칸이나 동전이 있는 칸으로는 이동 가능
  3. 벽일 때는 이동 불가
  4. 이동 횟수가 10번을 넘으면 중지하고 -1 반환

  <br>[입출력 예시]<br>board: [['.', '#'], ['.', '#'], ['.', '#'], ['o', '#'], ['o', '#'], ['#', '#']]<br>결과: 4

```java
public class Practice4 {
    final static int[][] dirs = {
        {1, 0}, {-1, 0}, {0, 1}, {0, -1}
    };
    static int cnt;

    static class Coin {
        int x;
        int y;

        public Coin(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }

    public static void solution(char[][] board) {
        if (board == null || board.length == 0 || board[0].length == 0) {
            return;
        }

        int n = board.length;
        int m = board[0].length;
        cnt = Integer.MAX_VALUE;

        ArrayList<Coin> coins = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (board[i][j] == 'o') {
                    coins.add(new Coin(j, i));
                }
            }
        }

        Coin coin1 = coins.get(0);
        Coin coin2 = coins.get(1);
        backTracking(board, m, n, coin1.x, coin1.y, coin2.x, coin2.y, 0);
        System.out.println(cnt == Integer.MAX_VALUE ? -1 : cnt);
    }

    public static void backTracking(char[][] board, int m, int n, int x1, int y1, int x2, int y2, int moveCnt) {
        if (moveCnt >= 10) {
            return;
        }

        for (int[] dir : dirs) {
            int x1Next = x1 + dir[0];
            int y1Next = y1 + dir[1];

            int x2Next = x2 + dir[0];
            int y2Next = y2 + dir[1];

            int dropCnt = 0;

            if (x1Next < 0 || x1Next >= m || y1Next < 0 || y1Next >= n) {
                dropCnt += 1;
            }

            if (x2Next < 0 || x2Next >= m || y2Next < 0 || y2Next >= n) {
                dropCnt += 1;
            }

            if (dropCnt == 2) {
                continue;
            }

            if (dropCnt == 1) {
                cnt = Math.min(cnt, moveCnt + 1);
                return;
            }

            if (board[y1Next][x1Next] == '#') {
                x1Next = x1;
                y1Next = y1;

            }
            if (board[y2Next][x2Next] == '#') {
                x2Next = x2;
                y2Next = y2;

            }

            backTracking(board, m, n, x1Next, y1Next, x2Next, y2Next, moveCnt + 1);
        }
    }
}
```



