---
title:  "[Java] 컬렉션 프레임워크(Collections Framework)"
excerpt: "자바 컬렉션 정리"
permalink: /categories/java/collections
author_profile: true
categories:
  - Java
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2021-03-29
toc: true
toc_sticky: true
---  

# 컬렉션 프레임웍(Collections Framework)
> 다수의 데이터를 다루는 데 필요한 다양한 클래스들을 제공  
* 인터페이스와 다형성을 이용한 객체지향적 설계  
* 재사용성이 높은 코드를 작성할 수 있음  

# 1. 핵심 인터페이스 3가지  
> 컬렉션을 다루는데 필요한 기능을 가진 3개의 인터페이스  
> List, Set, Map  
* Collection 인터페이스를 상속받는 List,Set와 Map이 있다.  

![collections](/assets/images/collections.png)  
* List를 구현하는 클래스들은 ArrayList, Vector, LinkedList  
* Set을 구현하는 클래스들은 HashSet, LinkedHashSet, TreeSet  
* Map을 구현하는 클래스들은 HashMap, Hashtable, TreeMap  

|인터페이스|특징|구현 클래스|  
|:---:|:---:|:---:|  
|List|순서가 있는 데이터의 집합, 중복 허용O|ArrayList, LinkedList, Stack, Vector 등|  
|Set|순서가 없는 데이터 집합, 중복 허용 X|HashSet, TreeSet 등|  
|Map|키와 값의 쌍으로 이루어진 데이터 집합, 순서가 없고 키는 중복 허용X, 값은 중복 허용O|HashMap, TreeMap, Hashtable, Properties 등|  

  
# 2. 컬렉션 클래스  
## ArrayList  
> Object배열을 이용해서 데이터를 순차적으로 저장하고 중복을 허용한다.  



## LinkedList  
## Stack과 Queue  
## Iterator, Literator, Enumeration  
## Arrays
## Comparator과 Comparable  
## HashSet  
## TreeSet   
## HashMap과 Hashtable  
## TreeMap
## Properties






