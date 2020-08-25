---
title:  "[Java]"
excerpt: "Java 개념 총정리 02"
permalink: /categories/java/java-Concept02
author_profile: true
categories:
  - Java
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2020-08-23
toc: true
toc_sticky: true
---

# Collection API  
다수의 데이터를 쉽고 효과적으로 처리할 수 있는 클래스의 집합이다.    
순서가 있는가, 중복을 허용하는가를 기준으로 적절한 Collection을 선택한다.   
![collectionsApi](/assets/images/collectionsApi.png)  
`ArrayList`는 순차적으로 삽입하는 경우 유리하고, `LinkedList`는 삽입을 통해 순서가 변경되었을 때 유리하다.  

## HashSet
두 객체의 중복 여부를 체크할 때 List계열보다 엄격하다.  
Object클래스의 `hashCode()`를 이용하여 그 값이 같은 경우에 같은 객체로 인식한다.  
<br/>

# Exception개념과 실행   
* 자바에서 발생하는 모든 예외 객체의 부모 클래스는 `Throwable`이지만 보통은 `Exception`타입으로 자식 객체들을 자주 처리한다.  
* 예외에는 `체크예외`와 `비체크예외`가 있다.  

## 1. 체크예외  
외적인 요인에 의해 발생하는 예외이고 `컴파일에러`가 발생한다.    
`Exception`클래스들  

## 2. 비체크예외  
프로그래머의 실수로 발생하는 예외  
`RuntimeException`클래스들  
ex) NullpointException, IndexOutoutException, ArthimeticException...  

## 에러의 종류 3가지  
**1. 컴파일에러**  
문법이 틀린 경우에도 에러 잡기가 비교적 쉽다.  
**2. 런타임(실행시간) 에러**  
컴파일과정에서는 잡히지 않는다.  
**3. 논리오류**  
가장 골치아픈 에러이다.  

## 멀티 catch 블럭
* `JDK1.7`부터 여러 catch블럭을 |기호를 이용해서 하나의 catch 블럭으로 합칠 수 있다.  
* finally블럭은 예외 발생과 상관없이 항상 실행된다.  

```java
try{
  //예외 발생할 가능성이 있는 문장을 넣음

}catch(Exception | Exception e){
  //예외처리를 위한 문장 넣음
  e.printTsatckTrace(); //예외에 대한 정보 출력

} finally{
  //예외 발생에 관계없이 항상 수행되어야 하는 문장들을 넣음

}
```  


## 메소드에 예외 선언  
`throws`키워드를 사용한다.  
```java
void method() throws Exception1, Exception2, ... ExceptionN {
...
}
```  

## 예외 발생 시키기  
* `new연산자`를 이용해 발생시키려는 예외 클래스 객체를 만들고 `throw e`를 이용해 예외를 발생시킨다.  
* 2번처럼 한줄에 객체 생성 및 throw까지 할 수 있다.  

```java
public static void main(String[] args){
  try{
    //1. new 연산자 이용해 객체를 생성한다.
    Exception e = new Exception("error");
    throw e;

    //2. 
    throw new Exception("error");
  }catch(Exception ex){
    ex.printStackTrace();
  }
}
```

* `finally`에 보통 자원을 반납하지만 최근에 `AutoCloseable`제공해서 스스로 `close()`할 수 있는 능력을 가지고 있다.  

# Thread개념과 실행  



# FILE IO개념
* 자바에서 File을 읽고 쓰는 것은 데이터를 JVM에 읽어들인 후, 다시 File로 쓰는 과정이다.
* 데이터의 시작과 끝이 있고 이 양쪽을 `Node`라고 부르고, 데이터의 흐름을 Stream이라고 한다.  
* 데이터의 타입에 따라, 노트 타입에 따라 최종 노트 스트림이 결정된다.  

## 스트림에 따라 분류
* 문자: Reader, Writer  
* 바이트(비문자): InputStream, OutputStream  

위 스트림 생성 후 추가 사용할 수 있다.  
## 보조 스트림  
* BufferedWriter, BufferedReader
* ObjectOutputStream(직렬화: 객체를 스트림으로), ObjectInputStream(역직렬화)

# TCP/UDP개념
W

# Network API
# JDBC API
# XML 파서: SAX와 DOM