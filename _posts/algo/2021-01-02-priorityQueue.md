---
title:  "[자료구조] 우선순위큐(Priority Queue)"
permalink: /categories/algo/priorityqueue
author_profile: true
categories:
  - 자료구조와 알고리즘
tags:
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2021-01-02
toc: true
toc_sticky: true
---
# 개념

들어간 순서에 상관 없이 **우선순위가 가장 높은 데이터**가 가장 먼저 나온다.  

- 기본적으로 숫자가 낮을 수록 우선순위가 높다. ⇒ 최소 힙  
- 일반적으로 힙으로 구현함  
- 큐 클래스 처럼 `add()`, `peek()`, `poll()` 등의 메소드 사용이 가능하다.  
- **예시)** 병원의 응급환자  

# 구현

> `java.util.PriorityQueue` 임포트 하여 사용한다.

## 1. PriorityQueue(우선순위큐)

---

```java
PriorityQueue<Integer> queue = new PriorityQueue<>();

priorityQueue.add(3);
priorityQueue.add(2);
priorityQueue.add(1);

System.out.println(queue.poll()); //1 출력
```

### 우선순위 변경

> 1. 우선순위큐 생성 시 Collections.reverseOrder() 사용
2. Comparator나 Comparable인터페이스 사용

우선순위 큐를 생성할 때, `collections.reverseOrder()`을 사용해 숫자가 높은 순으로 우선순위를 변경할 수 있다.

```java
PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(Collections.reverseOrder());

priorityQueue.add(3);
priorityQueue.add(2);
priorityQueue.add(1);

Integer poll = priorityQueue.
System.out.println(poll); //3 출력
```

 우선순위 큐를 생성할 때, `Comparator`를 생성하거나, 클래스 생성 시 `Comparable`를 구현해서 우선순위를 변경할 수 있다.

```java
PriorityQueue<Integer> queue = new PriorityQueue<>(new Comparator<Integer>() {

            @Override
            public int compare(Integer o1, Integer o2) { //절대값이 가장 작은값 출력
                if((Math.abs(o1) == Math.abs(o2) && o1>o2) || Math.abs(o1) > Math.abs(o2)) return 1;
                else return -1;
            }
        })
```