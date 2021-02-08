---
title:  "[Maven] 빌드 시 테스트파일 제외하기"
permalink: /categories/spring/deploy_remove_testfile
author_profile: true
categories:
  - Spring
tags:
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2021-02-08
toc: true
toc_sticky: true
---  


maven 빌드 시 테스트파일때문에 종종 에러가 나는 경우가 있다.  
분명 sts에서 돌렸을때는 잡히지 않았던 오류가 빌드파일 생성시 나타난다면 다음 방법을 시도해볼만하다.   
방법은 총 3가지가 있는데 이 중 하나 선택하면 된다. 나는 3번으로 하니 더이상 빌드fail이 뜨지 않았다.  

## 방법1  
빌드 시 커맨드라인에 다음 명령어를 입력해준다.   
```bash
package -Dmaven.test.skip=true  
```    

## 방법2  
```bash  
package -DskipTests
```    

## 방법3  
pom.xml에 다음 플러그인을 추가해준다.  
```bash
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-surefire-plugin</artifactId>
  <configuration>
    <skipTests>true</skipTests>
  </configuration>
</plugin>
```  