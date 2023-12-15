---
title: 2023.DEC.13(WED) JAVA DAY8_배열에 학생 점수 저장하고 접근하기_static
categories: [TIL(Today I Learned), SuperCoding_JAVA]
tags: [todayilearned, til, algorithm]
---

## ✅ Daily Report

### 📌 **TO-DO LIST**

- [x] submit github blog post
- [x] lesson 32, 33
- [x] assigment: 배열에 학생 점수 추가
      <br>
      <br>

## ✅ 배열에 학생 점수 추가하기

메인코드는 주어졌고 studentScore class구현이 목표

### [Main code]

```java
package day8_studentScore;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        System.out.println("학생들이 아무도 없을 때, 전체 시험 점수: " + Arrays.toString(StudentScore.getAllScores()));

        StudentScore student1 = new StudentScore(85);

        System.out.println("학생이 한명 추가 되었을 떄, 전체 시험 점수: " + Arrays.toString(StudentScore.getAllScores()));

        StudentScore student2 = new StudentScore(90);
        StudentScore student3 = new StudentScore(77);

        System.out.println("여러 명 추가후 전체 시험 점수: " + Arrays.toString(StudentScore.getAllScores()));

        student1.setScore(95);
        student2.setScore(88);
        student3.setScore(55);

        System.out.println("변경된 전체 시험 점수: " + Arrays.toString(StudentScore.getAllScores()));

        StudentScore student4 = new StudentScore(20);

        System.out.println("추가후 전체 시험 점수: " + Arrays.toString(StudentScore.getAllScores()));

        System.out.println("Student1 점수: " + student1.getScore());
        System.out.println("Student2 점수: " + student2.getScore());
        System.out.println("Student3 점수: " + student3.getScore());
        System.out.println("Student4 점수: " + student4.getScore());
    }
}


```

### [Student Score class code]

```java
public class StudentScore {
    // static
    private static int serialIndex;
    private static int[] allScores;


    public static int[] getAllScores() {
        return allScores;
    }
    private static void makeArray(int score){
        allScores= new int[]{score};
    }

    private static void addAllScore(int score) {
        if(allScores == null){
            makeArray(score);
            return;
        }
        int arrLength= allScores.length;
        allScores= Arrays.copyOf(allScores, arrLength+1);
        allScores[arrLength]= score;
    }

//myIndex통해서 학생 점수에 접근하기
    private int myIndex;
    private int score;

    public int getScore() {
        return score;
    }

    public void setScore(int score) {
        this.score= score;
        allScores[myIndex]= score;
    }
    public StudentScore(int score) {
        this.myIndex= serialIndex++;
        this.score= score;
        addAllScore(score);

    }
}


[ 예상 출력 ]

// 학생들이 아무도 없을 때, 전체 시험 점수: null
// 학생이 한명 추가 되었을 떄, 전체 시험 점수: [85]
// 여러 명 추가후 전체 시험 점수: [85, 90, 77]
// 변경된 전체 시험 점수: [95, 88, 55]
// 추가후 전체 시험 점수: [95, 88, 55, 20]
// Student1 점수: 95
// Student2 점수: 88
// Student3 점수: 55
// Student4 점수: 20
```
