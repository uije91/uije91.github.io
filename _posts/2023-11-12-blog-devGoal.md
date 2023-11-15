---
title:  "나는 어떤 개발자가 되고싶은가?"
category: blog
tag: ["제로베이스","백엔드","Java","Spring","개발자","백엔드공부","백엔드스쿨"]
typora-root-url: ../
---

# <br>나는 어떤 개발자가 되고싶은가?





```java
//TEST CODE
import java.util.InputMismatchException;
import java.util.Scanner;

public class _08_tax {
    static long pay = 0;

    static long inputTax() {
        Scanner sc = new Scanner(System.in);
        System.out.println("[과세금액 계산 프로그램]");
        while (true) {
            try {
                System.out.print("연소득을 입력해 주세요.:");
                pay = sc.nextLong();
                if (pay < 0) {
                    System.out.println("0이상의 값을 입력 해주세요.");
                    sc.nextLine();
                    continue;
                }
                break;
            } catch (InputMismatchException e) {
                System.out.println("0이상의 숫자를 입력 해주세요.");
                sc.nextLine();
            }
        }
        return pay;
    }

    static void resultTax() {
        int tax = 0;
        int dTax = 0;

        int[] taxBase = {12000000, 46000000, 88000000, 150000000, 300000000, 500000000, 1000000000};
        int[] taxRate = {6, 15, 24, 35, 38, 40, 42, 45};
        int[] deduction = {0, 1080000, 5220000, 14900000, 19400000, 25400000, 35400000, 65400000};

        if (pay <= taxBase[0]) {
            tax += calcTax(pay, taxRate[0]);
        } else if (pay <= taxBase[1]) {
            tax = calcTax(pay, taxRate[0]);
            tax += calcTax(pay, taxBase[0], taxRate[1]);
            dTax = calcDTax(pay, deduction[1], taxRate[1]);
        } else if (pay <= taxBase[6]) {
            tax = calcTax(pay, taxRate[0]);
            for (int i = 1; i < taxBase.length; i++) {
                tax += calcTax(taxBase[i - 1], taxBase[i - 2], taxRate[i - 1]);
                if (pay <= taxBase[i]) {
                    tax += calcTax(pay, taxBase[i - 1], taxRate[i]);
                    dTax = calcDTax(pay, deduction[i], taxRate[i]);
                    break;
                }
            }
        } else {
            tax = calcTax(pay, taxRate[0]);
            for (int i = 1; i < taxBase.length; i++) {
                tax += calcTax(taxBase[i], taxBase[i - 1], taxRate[i]);
            }
            tax += calcTax(pay, taxBase[taxBase.length - 1], taxRate[taxRate.length - 1]);
            dTax = calcDTax(pay, deduction[deduction.length - 1], taxRate[taxRate.length - 1]);
        }

        System.out.println();
        System.out.printf("[세율에 의한 세금]:\t\t\t%5d\n", tax);
        System.out.printf("[누진 공제 계산에 의한 세금]:\t%5d", dTax);
    }

    public static int calcTax(long pay, int taxRate) {
        int max = 12000000;
        int result;
        if (pay <= max) {
            result = (int) (pay * (taxRate * 0.01));
            System.out.printf(" %10d * %2d%% = %10d\n", pay, taxRate, result);
        } else {
            result = (int) (max * (taxRate * 0.01));
            System.out.printf(" %10d * %2d%% = %10d\n", max, taxRate, result);
        }
        return result;
    }

    public static int calcTax(long pay, int taxBase, int taxRate) {
        int result = (int) ((pay - taxBase) * (taxRate * 0.01));
        System.out.printf(" %10d * %2d%% = %10d\n", pay - taxBase, taxRate, result);
        return result;
    }

    public static int calcDTax(long pay, int deduction, int taxRate) {
        return (int) ((pay * (taxRate * 0.01)) - deduction);
    }

    public static void main(String[] args) {
        inputTax();
        resultTax();
    }
}
```

