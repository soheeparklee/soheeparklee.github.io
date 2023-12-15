---
title: 2023.DEC.12(TUE) JAVA DAY7_배열에 학생 추가, 삭제, 검색
categories: [TIL(Today I Learned), SuperCoding_JAVA]
tags: [todayilearned, til, algorithm]
---

## ✅ Daily Report

### 📌 **TO-DO LIST**

- [x] submit github blog post
- [x] lesson 28, 29, 30, 31
- [x] assigment: 학생 관리 시스템 구축하기
      <br>
      <br>

## ✅ Today I Learned

학생 데이터베이스를 만들어 학생 추가, 검색, 삭제

```java
public class Main {
    public static void main(String[] args){
        // 학생 정보 관리 시스템 객체 생성 (최대 2명 저장 가능)
        StudentManagementSystem system = new StudentManagementSystem(2);

        // 학생 추가
        Student student1 = new Student("홍길동", 12345, "컴퓨터공학", 3);
        system.addStudent(student1);

        // 학생 추가
        Student student2 = new Student("이순신", 67890, "수학", 2);
        system.addStudent(student2);

        System.out.println("학생 검색 시작하겠습니다.");
        // 학생 검색
        system.searchStudent(12345);

        System.out.println("학생 검색 삭제하겠습니다.");
        // 학생 삭제
        system.removeStudent(student1);

        System.out.println("학생 검색 시작하겠습니다.");
        // 학생 검색 (삭제된 학생)
        system.searchStudent(12345);

    }
}

public class Student {
    //field
    private String name;
    private int studentID;
    private String major;
    private int grade;

    //constructor

    public Student(String name, int studentID, String major, int grade) {
        this.name = name;
        this.studentID = studentID;
        this.major = major;
        this.grade = grade;
    }

    //getter and setter
    //getter, setter필요한 이유는 나중에 그 값만 받아오고 싶기 때문이다.
    public String getName() {
        return this.name;
    }

    public int getStudentID() {
        return this.studentID;
    }

    public String getMajor() {
        return this.major;
    }

    public int getGrade() {
        return this.grade;
    }

    public void setMajor(String major) {
        this.major = major;
    }

    public void setGrade(int grade) {
        this.grade = grade;
    }


}

public class StudentManagementSystem {

    private Student[] studentArr;

    private int arrSize;
    //constructor
    public StudentManagementSystem(int capacity){
        this.studentArr= new Student[capacity];
        this.arrSize = 0;
    }

    //method
    public void addStudent(Student student){
        if(arrSize < studentArr.length){
            studentArr[arrSize]= student;
            arrSize++;
            System.out.printf("학생 추가: %s%n", student.getName());
        }else{
            System.out.println("학생 데이터베이스가 꽉 찼습니다.");
        }

    }

    public void searchStudent(int studentID){
        for(int i=0; i<arrSize; i++){
            if(studentArr[i].getStudentID() == studentID){
                System.out.println("학생을 찾았습니다:");
                System.out.println("학생 이름:"+ studentArr[i].getName());
                System.out.println("학생 전공:"+ studentArr[i].getMajor());
                System.out.println("학생 학년:"+ studentArr[i].getGrade());
                return;
            }
        }System.out.println("학생을 찾을 수 없습니다. ");
    }

    public void removeStudent(Student student){
        for(int i=0; i<arrSize; i++){
            if(studentArr[i] == student){
                // 왼쪽으로 요소들을 이동
                for(int j=i; j<arrSize-1; j++){
                    studentArr[j] = studentArr[j+1];
                }
                studentArr[arrSize-1]= null;
                arrSize--;
                System.out.println("힉셍 삭제:" + student.getName());
                return;
            }
        }
        System.out.println("학생을 삭제할 수 없습니다");
    }
}


```
