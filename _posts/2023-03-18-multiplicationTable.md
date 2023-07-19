---
title: "[java] 구구단"
excerpt: "구구단"

categories:
  - java
tags:
  - [java]

permalink: /java/multiplicationTable/

toc: false

date: 2023-03-18
last_modified_at: 2023-03-18
---

아기는 만 3~5개월 경 뒤집기를 합니다. 뒤집기는 별거 아닌 것 같지만 아기에게는 큰 일입니다. 뒤집기를 하기 위해 하루종일 낑낑 거리거나 짜증을 내거나 울기까지 합니다. 힘들고 귀찮은 일이지만 살아가기 위해서는 반드시 해야 하는 일입니다. '뒤집기'라는 일을 마치고 나면 걸을 수 있고 말을 할 수 있게 됩니다. 위대한 일의 시작은 사소한 일입니다.

프로그래밍 언어를 배우면 반복문을 배웁니다. 반복문을 별거 아닌 것 같지만 개발자에게 중요한 일입니다. 대부분의 책에서는 배운 반복문을 적용하기 위해 구구단 출력하기 문제를 냅니다.

구구단 출력하기는 뒤집기와 비슷합니다. 사소한 코드이지만 이것들이 모여 위대한 코드가 될 겁니다.

![multiplicationTable](/assets/images/posts_img/multiplicationTable.png)

## 구구단

사용자에게 입력값을 받아 해당 입력값에 해당하는 구구단을 출력합니다.

```java
public class ExamJAVA {
    public static void gugudan(int dan, int end) {
        int i = dan;
        if (end < 0 || end >= 100) {
            System.out.println("end는 0보다 크고 100보다 작아야 합니다.");
        } else {
            System.out.println("===" + i + "단 입니다" + "===");
            for (int j = 1; j <= end; j++) {
                System.out.println(i + " X " + j + " = " + (i * j));
            }
        }
    }

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        System.out.println("시작 값을 입력하세요.");
        int startValue = input.nextInt();

        System.out.println("종료 값을 입력하세요.");
        int endValue = input.nextInt();

        gugudan(startValue, endValue);

        input.close();
    }
}

```

## 구구단2

사용자에게 입력값을 받지 않고 1단부터 9단까지의 구구단을 출력합니다.

```java
        for (int j = 2; j <= 9; j++) {
            System.out.println("=====" + j + "단=====");
            for (int i = 1; i <= 9; i++) {
                System.out.println(j + " X " + i + "= " + i * j);
            }
        }
```
