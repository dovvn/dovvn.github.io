---
title:  "[Java] Char형을 Int형으로 바꾸기"
excerpt: "char -'0', Character.getNumericValue(s.charAt(i))"
permalink: /categories/java/java-charToint
author_profile: true
categories:
  - Java
tags:
  - 알고리즘 기본개념
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2020-08-03
toc: true
toc_sticky: true
---

# 1. char -'0'
char는 int형으로 넘어갈 때 아스키코드를 넘기기 때문에 0(아스키코드 32)만큼 빼주면 원하는 숫자를 얻을 수 있다.

```java
int a = s.charAt(j) - '0';
```

# 2. Character.getNumericValue(s.charAt(i))
```java
int a = Character.getNumericValue(s.charAt(i))
```
