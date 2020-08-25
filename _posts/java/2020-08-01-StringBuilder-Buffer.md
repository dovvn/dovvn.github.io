---
title:  "[Java] StringBuilder와 StringBuffer"
excerpt: "표준입출력, BufferedReader, BufferedWriter, Scanner"
permalink: /categories/java/StringBuilder-Buffer
author_profile: true
categories:
  - Java
tags:
  - 알고리즘 기본개념
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2020-08-01
toc: true
toc_sticky: true
---

# StringBuffer, StringBuilder을 사용하는 이유
자바에서 문자열을 다루는 대표적인 클래스로 `String, StringBuffer, StringBuilder`가 있다.  
그 중 생소한 StringBuffer와 StringBuilder에 대해 정리해보고자 한다.   

String클래스는 지정된 문자열을 수정할 수 없다.  
예를 들어 아래와 같은 코드를 작성한다면,
```java
String s = "hello";
s += "hello world";
```
여기서 s값이 수정된것으로 보이지만 그렇지 않다. s가 "hello"라는 메모리영역을 참조하다가 두번째 줄이 실행되면서 "hello world"가 들어있는 메모리를 참조하게 되고 원래 가리키던 "hello" 메모리는 Garbage로 남게 되어 이후 GC에 의해 처리된다.  
즉, 문자열을 수정은 불가능하도 새로운 String인스턴스를 생성하게 된다.  
이렇게 새로 생기는 String을 방지하기 위해 StringBuffer, StringBuilder를 사용하게 되는 것이다.

<br/>

# StringBuffer와 StringBuilder
StringBuffer, StringBuilder둘다 객체를 만든 후 .append(), .delete() 메소드를 사용해 문자열을 추가, 수정, 삭제할 수 있다. 즉, 동일한 문자열에서 데이터 처리를 원하는 경우 이 두가지 클래스를 사용하는 것이 좋다.  
```java
StringBuffer sb = new StringBuffer();
		sb.append("String");
		sb.append(" Buffer");
		System.out.println(sb);
```
![syste-in.png](/assets/images/stringbuilder.PNG)    

<br/>

```java
StringBuilder sb = new StringBuilder();
		sb.append("String");
		sb.append(" Builder");
		System.out.println(sb);
```
![syste-in.png](/assets/images/stringbuffer.PNG)    

<br/>

# StringBuffer와 StringBuilder의 차이점
StringBuffer은 멀티스레드 환경에서 사용할 수 있으나, StringBuilder은 동기화를 지원하지 않아 멀티스레드 환경에서는 사용할 수 없다. 하지만 싱글스레드 환경에서는 StringBuilder의 성능이 더 뛰어나다.

## 참고
여기서 **스레드**란?
하나의 프로세스(실행중인 프로그램) 내부에서 독립적으로 실행되는 하나의 작업 단위이다.    
프로세스는 프로그램 수행에 필요한 데이터, 메모리, 쓰레드 등으로 구성되어 있다.  
모든 프로세스에는 하나 이상의 스레드가 존재하며 여러개의 스레드 환경을 바로 멀티스레드라 하고 동시에 여러개의 일을 할 수 있게 된다. 스레드와 관련된 문서는 추후 자세하게 작성할 예정이다.  

