---
title: "[java] 최대값·최소값·중앙값"
excerpt: "최대값·최소값·중앙값"

categories:
  - java
tags:
  - [java]

permalink: /java/calculateWithJava/

toc: true


date: 2023-03-20
last_modified_at: 2023-03-20
---

다른 사람의 이름을 잘못 부르면 처음에는 그러려니 할 수 있습니다. 그러나 계속된다면 그 사람에게 실례입니다. 정확히 그 사람 이름대로 불러야 합니다.

프로그래밍을 하다보면 '매개변수'를 자주 사용합니다. 그런데 매개변수에도 정확한 이름이 있습니다. 처음에는 그러려니 넘길 수 있지만 계속된다면 매개변수한테 미안한 일입니다. 정확한 이름으로 매개변수를 불러야 합니다.

메서드를 정의할 때 사용하는 매개변수를 '매개변수' 혹은 '형식매개변수'라고 합니다. 형식매개변수는 '가인수(임시인수)'라고 합니다. 메서드를 호출할 때 사용하는 매개변수의 값을 '실인수'라고 합니다. 정리하자면 메서드를 정의할 때는 '매개변수' 메서드를 호출할 때는 '실인수'입니다.

![calculateWithJava](/assets/images/posts_img/calculateWithJava.png)

## 최대값 구하기

메서드로 분리하지 않고 main함수에서 바로 실행합니다.

```java
public class Max3 {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        System.out.println("세 정수의 최대값을 구합니다.");

        System.out.print("a의 값: ");
        int a = input.nextInt();

        System.out.print("b의 값: ");
        int b = input.nextInt();

        System.out.print("c의 값: ");
        int c = input.nextInt();

        int max = a;

        if (b > max) {
            max = b;
        }

        if (c > max) {
            max = c;
        }

        System.out.println("최대값은 " + max + "입니다.");
    }
}

```

### 메서드 분리

```java
public class Max3m {

    static int max3(int a, int b, int c) {
        int max = a;
        if (b > max) {
            max = b;
        }

        if (c > max) {
            max = c;
        }

        return max;
    }

    public static void main(String[] args) {

        System.out.println("max(3, 2, 1) = " + max3(3, 2, 1));
    }
}

```

## 최소값 구하기

```java
package org.example;

import java.util.Scanner;

public class Min3 {
        static int min3(int a, int b, int c) {
            int min = a;
            if (b < min) min = b;
            if (c < min) min = c;

            return min;
        }

        public static void main(String[] args) {
            Scanner input = new Scanner(System.in);
            int a, b, c;

            System.out.println("세 정수의 최소값을 구합니다.");
            System.out.print("a의 값 : ");
            a = input.nextInt();

            System.out.print("b의 값 : ");
            b = input.nextInt();

            System.out.print("c의 값 : ");
            c = input.nextInt();

            int min = min3(a, b, c);

            System.out.println("최소값은 " + min + "입니다.");
        }
    }

```

## 중앙값 구하기

```java
public class Median {

    static int med3(int a, int b, int c) {
        if (a >=b) {
            if (b >= c) {
                return b;
            } else if (a <= c) {
                return a;
            } else {
                return c;
            }
        } else if (a > c) {
            return a;
        } else if (b > c) {
            return c;
        } else {
            return b;
        }
    }

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        System.out.println("세 정수의 중앙값을 구합니다.");

        System.out.print("a의 값: ");
        int a = input.nextInt();

        System.out.print("b의 값: ");
        int b = input.nextInt();

        System.out.print("c의 값: ");
        int c = input.nextInt();

        System.out.println("중앙값은 " + med3(a, b, c) + "입니다.");
    }
}
```

<br>

---

## 참고문헌

**Do it! 자료구조와 함께 배우는 알고리즘 입문: 자바 편**

BohYoh Shibata 지음ㅣ이지스 퍼블리싱ㅣ2022ㅣ[**도서 정보**](https://product.kyobobook.co.kr/detail/S000061352392)
