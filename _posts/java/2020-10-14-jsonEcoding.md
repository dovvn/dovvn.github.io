---
title:  "[JSP/Servlet] Servlet에서 Ajax로 JSON 응답할 때 한글 깨짐 해결방법"
permalink: /categories/java/jsonEncoding
author_profile: true
categories:
  - Java
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2020-10-14
toc: true
toc_sticky: true
---

클라이언트에서 제이쿼리 요청을 받아서 서블릿에서 처리 후 json데이터를 다시 응답하려고 할때 한글 데이터가 포함되어 있는 경우 ???와 같이 제대로 받지 못하게 된다.  

이럴 경우 Servlet과 응답을 받는 페이지에 아래 코드를 추가해주어야 한다.

### Serlvet 페이지  
```java
Gson gs = new Gson();
String result = gs.toJson(commentList);
System.out.println(result); 

resp.setContentType("text/json; charset=utf-8"); //★추가!!
resp.getWriter().write(result);
```  

### JSP 페이지(응답 받는 페이지)  
```java
.
.
.
$.ajax({
			url: 'comment.do',
			data: {'action':'commentList', 'bnum':'${dto.bnum}'},
			method: 'get',
			contentType: "text/json; charset=UTF-8", //★추가!!
      .
      .
})
.
.
.
```



