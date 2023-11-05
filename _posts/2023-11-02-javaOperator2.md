---
title:  "자바(Java)-여러가지 연산자(2)"
category: java
toc: true
toc_label: "이진수와 비트연산자"
toc_sticky: true
typora-root-url: ../
---





## 이진법

- 이진법은 우리가 사용하는 숫자(십진법) 과 다르게 컴퓨터에서 데이터 표현에 사용하는 방식입니다.
- 이진법은 0과 1 두 개의 수를 이용하여 숫자를 표현합니다.


<style>
    /* 기본 스타일 (데스크톱 화면) */
    div {
        margin-left: 20px;
        padding-left: 20px;
    }

    table {
        text-align: center;
    }

    th, td {
        padding: 5px;
    }

    tr {
        height: 20px;
    }

    /* 모바일 화면을 위한 미디어 쿼리 */
    @media screen and (max-width: 768px) {
        div {
            margin: auto;
            padding: auto;
        }

        table {
            width: 90%; /* 테이블을 화면 너비에 맞게 확장 */
        }

        th, td {
            padding: 2px; /* 셀 패딩 축소 */
        }

        tr {
            height: auto; /* 행 높이 자동으로 조정 */
        }
    }
</style>


<div>
    <table>
        <tr>
            <td>10진수</td>
            <td>0</td>
            <td>1</td>
            <td>2</td>
            <td>3</td>
            <td>4</td>
            <td>5</td>
            <td>6</td>
            <td>7</td>
            <td>8</td>
            <td>9</td>
            <td>10</td>
        </tr>
        <tr>
            <td>2진수</td>
            <td>0000</td>
            <td>0001</td>
            <td>0010</td>
            <td>0011</td>
            <td>0100</td>
            <td>0101</td>
            <td>0110</td>
            <td>0111</td>
            <td>1000</td>
            <td>1001</td>
            <td>1010</td>
        </tr>
    </table>
</div>
- 이진법에서 각 자리수는 우측부터 2<sup>0</sup>, 2<sup>1</sup>, 2<sup>2</sup>… 순을 의미합니다.


- 예를들어 10진수 5를 2진수로 표현하면 2<sup>2</sup>(4) + 2<sup>0</sup>(1) 인 101입니다.
- 이진법에서 양수와 음수를 판단하는 기준인 부호 비트는 제일 왼쪽에 있는 최상위 비트를 기준으로 하는데 부호 비트가 0이면 양수, 1이면 음수를 의미합니다. 





## 2의 보수

- 10진수에서 음수를 표현하고 싶을 때는 마이너스(-)기호를 사용하면 되지만, 2진수에서는 다른 방식으로 음수를 표현합니다. <br>그렇기 때문에 이진법에서 음수를 표현하고 싶을 때에는 2의 보수를 이용합니다.<br>예를 들어서 -5를 표현하고 싶다면 10진수 5의 2진수(0101) 을 <u>반전 후 1을 더한 값</u> 1011은 2의 보수입니다. (101의 반전 : 010 + 1)





## 비트 논리 연산자

- 각각의 비트 단위로 연산합니다.

- AND 연산자(&) : 두 개의 비트 값이 모두 1인 경우에만 결과 1 

![bit_and](/images/2023-11-02-004/bit_and.png)

- OR 연산자(\|) : 두 개의 비트 값 중 하나라도 1이면 결과 1

![bit_or](/images/2023-11-02-004/bit_or.png)

- XOR 연산자(^) : 두 개의 비트 값이 같으면 0, 다르면 1 

![bit_xor](/images/2023-11-02-004/bit_xor.png)

- NOT 연산자(\~) : 비트 값이 0이면 1로, 1이면 0으로 반전

![bit_not](/images/2023-11-02-004/bit_not.png)



- 이미지 출처 : [https://www.tcpschool.com/c/c_operator_bitwise](https://www.tcpschool.com/c/c_operator_bitwise)





## 비트 이동 연산자

- Left Shift 연산자(\<\<) : 비트를 왼쪽으로 이동합니다.
- Right Shift 연산자(\>\>) : 비트를 오른쪽으로 이동합니다.
  - 오른쪽으로 이동할 때 (\>\>) 는 기존의 비트 연산자의 부호 비트가 그대로 따라옵니다.
  - 하지만 (\>\>\>) 는 부호 비트의 값을 무조건 0으로 고정합니다. 

```java
int num1 = 8, num2 = -8;

System.out.println("<< 연산자에 의한 결과 : "+ (num1 << 1));	//결과 : 16 (곱셈 : num1 * 2^1)
System.out.println(">> 연산자에 의한 결과 : "+ (num2 >> 2));	//결과 : -2 (나눗셈 : num2 / 2^2)
System.out.println(">>> 연산자에 의한 결과 : "+ (num1 >>> 2));	//결과 : 2
System.out.println(">>> 연산자에 의한 결과 : "+ (num2 >>> 2));	//결과 : 1073741822
```

