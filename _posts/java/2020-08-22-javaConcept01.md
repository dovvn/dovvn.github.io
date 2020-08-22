---
title:  "[Java]"
excerpt: "Java 개념 총정리 01"
permalink: /categories/java/java-Concept01
author_profile: true
categories:
  - Java
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2020-08-22
---

# JAVA 배경 지식
## Java의 특징
Write Once, Run Anywhere  
* 자바는 JVM하고만 상호작용을 하기 때문에 OS와 하드웨어에 독립적이라 다른 OS에서도 변경 없이 실행 가능하다. 즉, JVM이 설치된 환경 어느곳이든 동작할 수 있다(크로스 플랫폼)

## Eclipe
Java개발의 대표적인 IDE이며 컴파일, 디버깅, 빌드등의 개발 전체 과정을 편리하게 관리해준다.

## Java 개발환경 구축하기
JDK, IDE다운로드 후 환경변수 설정(JAVA_HOME, Path) 해주고 이클립스 탭메뉴 Preference-Encoding검색하고 utf-8로 변경, html,css,jsp,xml모두 utf-8로 변경
* JDK(Java Development Kit): JVM + JRE, 자바 개발하는데 필요한 프로그램으로 구성
* JVM(Java Virtual Machine): 자바를 실행하기 위한 가상 기계
* JRE(Java Runtime Environment): 자바 실행 환경, 자바로 작성된 프로그램이 실행되기 위한 최소환경

## [Java API 문서](https://docs.oracle.com/javase/8/docs/api/)
클래스 라이브러리의 모든 클래스에 대한 설명이 자세하게 나와 있다.
자바의 사전이라고 생각하면 된다.

## Java 컴파일 과정
Hello.java →(javac.exe 컴파일)→ Hello.class 생성 → (java.exe 실행) → "Hello.world" 출력

<br/>

# 변수
## 변수의 타입
### 1. 기본형(Premitive Type)
실제값을 스택(비싸다, 가깝다)에 저장한다.   
선언하는 동시에 사이즈가 이미 정해져있다.    
종류는 총 8가지가 있다.  
![variable-type](/assets/images/variable-type.png)    

### 2. 참조형(reference Type)
가변적인 공간을 차지한다.
크기가 크기 때문에 별도로 힙(싸다, 멀다)이라는 메모리 공간에 실제값을 저장하고, 이 주소를 참조변수로 관리한다.  

```
String s1 = "hello";
String s2 = "hello";
String s3 = new String("hello");
String s4 = new String("hello");
```
s1과 s2는 같은 문자열을 담고 있으므로 힙의 같은 문자열을 참조한다. 따라서 주소값이 서로 같기 때문에 s1 == s2는 같다.

## 형변환(Type-Casting)
변수 또는 상수의 타입을 다른 타입으로 변환하는 것  
* 작은 타입에 큰 타입으로의 변환은 오류가 발생한다.  
* 정수형은 실수형으로 자동으로 형변환된다.  
* char타입은 문자의 유니코드(정수)가 저장되므로 int형에서 char형, char형에서 int형으로 형변환하게 되면 아스키코드표를 기준으로 변환한다.
* boolean을 제외한 나머지 7개 기본형은 서로 형변환이 가능하다.
* 기본형과 참조형은 서로 형변활할 수 없다.

<br/>

#  연산자
연산을 수행하기 위한 기호로 연산을 수행하기 위해서는 반드시 피연산자가 필요하다.
![operator](/assets/images/operator.png)  
## 비트연산자
피연산자를 비트단위로 논리 연산하며 피연산자로 오로지 정수만 올 수있다.   
피연산자를 이진수로 표현했을 때 |,&,^의 규칙에 따라 연산을 수행한다.  
* |(OR연산자): 피연산자 중 한 쪽의 값이 1이면, 1을 결과로 얻는다. 이 외에는 0을 얻는다.  
* &(AND연산자): 피연산자 양 쪽이 모두 1이어야만 1을 결과로 얻는다. 그 외에는 0을 얻는다.  
* ^(XOR연산자): 피연산자의 값이 서로 다를 경우에만 1을 결과로 얻는다. 같을때는 1을 얻는다.  
* ~(비트전환연산자): 피연산자를 ~로 표현했을 때, 0은 1로 1은 0으로 바꾼다. 논리부정연산자 '!'와 유사하다.
* <<, >>(쉬프트연산자): 피연산자의 각 자리를 왼쪽(<<)또는 오른쪽(>>)으로 이동한다. 예를 들어 `8<<2`는 피연산자인 10진수 8의 2진수를 왼쪽으로 2자리 이동한다. 이동 후 범위를 벗어난 값은 버려지고, 빈자리는 0으로 채워진다.  
* >>>: 부호를 신경쓰지 않고 오른쪽으로 이동한다.

## 조건연산자 ? :
조건식, 식1, 식2 모두 세개의 피연산자를 필요로 하는 삼항 연산자이다.  
조건식이 true이면 식1이 false이면 식2가 연산 결과가 된다.
```java
result = x > 0 ? 1 : (x == 0 ? = : -1) //이런식으로 중첩 가능
```

<br/>


