---
title:  "[Java] 이클립스로 디버깅하기"
excerpt: "이클립스로 디버깅하기"
permalink: /categories/java/eclipse-debuging
author_profile: true
categories:
  - Java
tags:
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2020-08-04
---

# 이클립스 디버깅하기  
에러가 발생하는 라인에 브레이크포인트를 걸어준 후 f11을 누르면 브레이크포인트가 걸린 부분에서 디버깅이   시작된다. 그럼 검사하는 줄을 기준으로 디버그를 진행할 수 있다.  
 
![breakpoint](/assets/images/breakpoint.PNG)     
브레이크 포인트를 걸어주고(마우스 더블클릭)   

![f11](/assets/images/f11.PNG)      
디버깅f11을 실행한 모습    

1. Step Into(F5): 한단계씩 수행  
2. Step Over(F6): 함수단위 수행  
1. Step Return(F7): 호출한 곳으로 돌아감  

<br/>

* Variables창  
![variables](/assets/images/variables.PNG)   
f5를 계속 눌러주면 변수의 상태를 확인할 수 있다. 조건문 등에서 유용하다.    

* BreakPoints  
![breakpoints](/assets/images/breakpoints.PNG)    
현재 프로젝트에서 걸려 있는 브레이크포인트 목록을 보여준다.    

* Expressions  
![expressions](/assets/images/expressions.PNG)     
알고싶은 변수를 작성한 후 수행하면 그 변수의 값을 확인할 수 있다.  
