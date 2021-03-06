---
title:  "[Spring] JSON 라이브러리/Spring에서 Ajax로 json응답하기"
excerpt: "GSON,Jackson 라이브러리"
permalink: /categories/spring/jsonlibrary
author_profile: true
categories:
  - Spring
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2020-10-21
toc: true
toc_sticky: true
---

> GSON, Jackson 라이브러리를 쓰는 방법 두가지가 있다.  

# GSON
스프링에서 Ajax로 부터 데이터 요청이 들어왔을 때 GSON,Jackson을 사용해서 응답 데이터를 json으로 바꾸는 방법을 공부해보았다.     
## 1. pom.xml
먼저 GSON 라이브러리 사용을 위해 pom.xml에 아래 의존성을 추가한다.  
```xml
		<dependency>
			<groupId>com.google.code.gson</groupId>
			<artifactId>gson</artifactId>
			<version>2.8.0</version>
		</dependency>

```

## 2. Controller  
Controller에서 Gson객체를 만들어서 응답할 데이터를 JSON Object로 바꾸고 이를 문자열로 바꿔서 제이쿼리에게 전달한다.  
```java
@GetMapping(value = "commentList.do", produces = "application/text; charset=utf8")
	@ResponseBody
	public String comment(@RequestParam("bnum") int bnum) {
		ArrayList<CommentDto> commentList = bservice.getCommentList(bnum);
		Gson gs = new Gson();
		return gs.toJson(commentList);
	}
```  

## 3. JQuery  
Controller의 반환형식이 String이었으므로 JQuery에서는 응답 받은 데이터를 `JSON.parse()`를 사용해서 JSON Object로 변환시켜주면 해당 프로퍼티에 접근할 수 있게 된다.  
```javascript
$.ajax({
		url: 'commentList.do', //요청할 서블릿
		data:{'bnum':'${Bdto.bnum}'},
		method: 'get',
		contentType: "text/json; charset=UTF-8",
		success: function(output){
		    var result = JSON.parse(output);
		    console.log(result[0]['cwriter']); 
            ..
        }
        ..
})
```  

# Jackson-databind Library
pom.xml에 다음 추가    
```xml
        <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.11.3</version>
        </dependency>
```  