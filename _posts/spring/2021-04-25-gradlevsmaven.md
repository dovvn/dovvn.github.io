---
title:  "[Spring] 빌드 관리 도구 Maven vs Gradle"
excerpt: "Maven과 Gradle 비교"  
permalink: /categories/spring/gradlevsmaven
author_profile: true
categories:
  - Spring
tags:
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2021-04-25
toc: true
toc_sticky: true
---   


# 빌드 관리 도구란?
> 자바 프로젝트의 빌드를 자동화해주는 빌드 툴  
빌드란 소스코드를 컴파일, 테스트, 정적 분석 하여 실행 가능한 애플리케이션으로 만들어주는 과정으로 이를 도와주는 도구가 '빌드 관리 도구'이다.    

* 라이브러리를 자동으로 추가하고 관리해준다.  
* 라이브러리 버전을 자동으로 동기화해준다.  

 ## Maven
 > pom.xml을 이용한 빌드 시스템  

 ## Gradle
 > Ant와 Maven의 장점을 살

 ### Gradle이 Maven보다 좋은 점
 **1. 유연함**
 * Maven의 `pom.xml`은 선언형으로 설정하는 정적인 문서이지만 Gradle의 `build.gradle`은 스크립트로 작성하는 동적인 소스 파일이다.  
 * 따라서, Maven은 어떤 설정이 필요할 때 한계가 있지만 Gradle은 로직을 넣을 수 있으니 한계가 없다. 로직 안에 플러그인을 호출하거나 직접 코드를 짜면 된다.  

 **2. 가독성**
 * Maven  

 * Gradle  



