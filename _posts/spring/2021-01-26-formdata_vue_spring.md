---
title:  "[Spring] Vue.js에서 SpringBoot로 multipart/form-data와 JSON 전송하기"
excerpt: "JSON데이터와 파일을 함께 axios요청하는 방법"
permalink: /categories/spring/formdata_vue_spring
author_profile: true
categories:
  - Spring
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2021-01-26
toc: true
toc_sticky: true
---
Vue.js에서 사진파일과 다른 피드 정보를 Spring Boot로 axios요청하려고 했는데 자꾸만 null값으로 오거나, 데이터 형식이 맞지 않다는 에러가 떠서 몇시간을 헤맸다 ㅠㅠㅠ     
다행히 아래 코드로 바로 해결할 수가 있었다.    

## 1. Vue.js 입력폼 만들기    
먼저 input태그를 활용해서 데이터를 보내줄 테이블을 만든다.     
테스트를 위해 나는 수정과 삭제하는 버튼을 같이 만들어 주었다.  
```html
<template>
    <div id="movie-add">
        <table id="movie-add-table">
            <label>사진파일
                <input type="file" id="file" ref="file" v-on:change="handleFileUpload()"/>
             </label>
            <tr>
              <th>피드번호(수정할때만)</th>
              <td><input type="text" v-model="feed.id"></td>
            </tr>
            <tr>
                <th>아이디</th>
                <td><input type="text" v-model="feed.userId"></td>
            </tr>
             <tr>
                <th>지역</th>
                <td><input type="text" v-model="feed.location"></td>
            </tr>
            <tr>
                <th>내용</th>
                <td><input type="text" v-model="feed.feedText"></td>
            </tr>
        </table>
        <button v-on:click="insertFeed()">피드 등록</button>
         <button v-on:click="modifyFeed()">피드 수정</button>
    </div>
</template>
```  

## 2. formData로 작성하기    
여기서 파일과 JSON데이터를 같이 보내주어야 하기 때문에 `FormData`안에 키와 값 쌍으로 담아주어야 한다.    
피드 정보`feed`는 JSON객체로 바로 보내면 백엔드에서 알 수 없기 때문에 `stringfy`를 이용해 객체를 String 객체로 변환하여 보내야한다.    

```javascript  
const formData = new FormData();
formData.append("file", this.file);
formData.append("feed", new Blob([JSON.stringify(this.feed)], { type: "application/json" }));

axios.post( 'http://localhost:7777/api/feed/', formData,{
    headers: {
        "Content-Type": `multipart/form-data`,
        }
    }).then(function(res){
          console.log(res.data);
    }).catch(function(){
          console.log('FAILURE!!');
});  
```  

만약, 여러개의 파일을 보내고 싶다면 동일한 key값으로 여러번 데이터를 추가해주면 된다.   
```javascript 
data.files.forEach((file) => formData.append("files", file)); 
```    

## 3. Spring Boot 컨트롤러 작성   
axios통신 준비가 완료되었다면, 전송할 url에 해당하는 컨트롤러를 만들어준다.   
이때 유의할 점은 ★반드시 `@RequestParam`으로 받아야한다. 아님 오류가 발생한다.   

```java  
	//피드에 글쓰기
	@ApiOperation(value="피드 작성", notes="피드 작성 성공시 true, 댓글 작성 실패시 false 반환", response = Boolean.class)
	@PostMapping(value="/feed")
	public void insertFeed(@ApiParam(value="피드 객체(feed)", required=true)@RequestPart FeedDto feed, @ApiParam(value = "사진 파일(file)", required = true) @RequestPart(value = "file", required = true) MultipartFile file) throws IOException {
		System.out.println(feed.toString());
        System.out.println(file.getOriginalFilename());
	}
```    
 
[실행 결과]    
피드정보와 파일 모두 잘 넘어오는 것을 확인할 수 있다.   
![multipart_result]](/assets/images/multipart_result.png)     


※ 참고
[pring Boot | multipart/form-data 파일 업로드 ( + React , Axios, REST API, multiple files)](https://gaemi606.tistory.com/m/162?category=745027)