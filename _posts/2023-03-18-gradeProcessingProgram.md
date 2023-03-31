---
title: "[java] 성적 처리 프로그램"
excerpt: "성적 처리 프로그램"

categories:
  - java
tags:
  - [java]

permalink: /java/gradeProcessingProgram/

toc: true
toc_sticky: true

date: 2023-03-18
last_modified_at: 2023-03-18
---

인생은 시험의 연속입니다. 초중고와 대학교에서는 중간·기말고사를 치르고 성인이 되어서는 입사 시험을 치릅니다. 입사 후에도 승진시험이나 업무에 필요한 시험을 치릅니다. 뿐만아니라 삶에서도 여러 시험이 있습니다. 인생이 끝나는 순간까지 시험은 계속됩니다. 인생 자체가 시험입니다. 시험에는 결과가 따르고 결과는 인생에 영향을 미칩니다.

5년차 개발자 선배와 같은 시험을 쳤습니다. 선배는 30분 만에 풀었고 저는 7시간 만에 풀었습니다. 나는 왜 이것밖에 안될까 라는 자조가 들었습니다. 한없이 작아졌습니다. 다음 시험이나 그 다음 시험에 제가 또 질 수도 있습니다. 그러나 아직 시험은 끝나지 않았습니다. 언젠가 제가 이기는 날도 올겁니다.

![commitConvention](/assets/images/posts_img/gradeProcessingProgram.png)

# 문제

① Math.random() 메서드를 활용하여 5명 학생에 대한 국어, 영어, 수학 점수를 60~100 사이 난수를 발생시켜 처리하시오.<br />
② 학생별 국어, 영어, 수학 점수의 합계를 출력하시오.<br />
③ 국어, 영어, 수학 점수의 합계를 이용하여 평균을 출력하시오.<br />
④ 평균은 소숫점 2자리에서 반올림하여 소숫점 1자리까지 표시되도록 처리하시오.<br />
⑤ 국어, 영어, 수학 점수의 합계를 이용하여 등수를 처리하시오.

# Source Code

```java

public class TestScore {

    String student1;
    String student2;
    String student3;
    String student4;
    String student5;

    public TestScore(String student1, String student2, String student3, String student4, String student5) {
        this.student1 = student1;
        this.student2 = student2;
        this.student3 = student3;
        this.student4 = student4;
        this.student5 = student5;
    }

    public void printScore() {

        int[][] score = new int[5][3];
        for (int i = 0; i < score.length; i++) {
            for (int j = 0; j < score[i].length; j++) {
                score[i][j] = (int) (Math.random() * (100 - 60 + 1) + 60);
            }
        }

        int[] sum = new int[5];
        for (int i = 0; i < score.length; i++) {
            for (int j = 0; j < score[i].length; j++) {
                sum[i] += score[i][j];
            }
        }
        double[] average = new double[5];
        for (int i = 0; i < average.length; i++) {
            average[i] = Math.round((double) (sum[i] / 3.0) * 100.0) / 100.0;
        }
        int[] rank = new int[5];
        for (int i = 0; i < rank.length; i++) {
            int temp = 1;
            for (int j = 0; j < rank.length; j++) {
                if (sum[j] > sum[i]) {
                    temp++;
                }
            }
            rank[i] = temp;
        }
        System.out.println("이름 " + "국어 " + "영어 " + "수학 " + "합계 " + "평균 " + "등수 ");
        System.out.println("========================================");
        System.out.println(this.student1 + "\t" + score[0][0] + "\t" + score[0][1] + "\t" + score[0][2] + "\t" + sum[0] + "\t" + average[0] + "\t" + rank[0]);
        System.out.println(this.student2 + "\t" + score[1][0] + "\t" + score[1][1] + "\t" + score[1][2] + "\t" + sum[1] + "\t" + average[1] + "\t" + rank[1]);
        System.out.println(this.student3 + "\t" + score[2][0] + "\t" + score[2][1] + "\t" + score[2][2] + "\t" + sum[2] + "\t" + average[2] + "\t" + rank[2]);
        System.out.println(this.student4 + "\t" + score[3][0] + "\t" + score[3][1] + "\t" + score[3][2] + "\t" + sum[3] + "\t" + average[3] + "\t" + rank[3]);
        System.out.println(this.student5 + "\t" + score[4][0] + "\t" + score[4][1] + "\t" + score[4][2] + "\t" + sum[4] + "\t" + average[4] + "\t" + rank[4]);
    }

    public static void main(String[] args) {

        TestScore testScore = new TestScore("고길동", "홍길동", "김철수", "오이지", "개나리");

        testScore.printScore();
    }
}

```
