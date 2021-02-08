---
title:  "[Nginx] Nginx로 웹서비스(Vue+Spring Boot) 배포하기"
permalink: /categories/spring/nginx_deploy
author_profile: true
categories:
  - Spring
tags:
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2021-02-06
toc: true
toc_sticky: true
---

Nginx를 사용해서 AWS EC2환경에 웹프로젝트를 배포하는 방법을 정리하려고 한다.  

## Nginx란?
> 아파치 톰캣과 같은 역할을 해주는 WAS로 가벼움과 높은 성능을 목표로 하는 웹 서버  

## Nginx 설치
먼저 발급된 키에 접속 후, 우분투환경에서 Nginx를 설치해준다.  
다음 명령어를 입력하여 새로 설치할 패키지들이 있는지 확인 후, 설치를 진행해준다.  
```bash
sudo apt-get update
sudo apt-get upgrdae
sudo apt-get install nginx
```  

## 환경 설정  
config파일을 설정해주기 위해 수정한다.  
만약 수정이 안된다면 `sudo vi default`를 입력해 읽기모드에서도 수정이 될 수 있도록 한다.  
```bash
cd /etc/nginx/sites-available
vi default
```  

![nginx_conf](/assets/images/nginx_conf.png)    


환경설정을 완료했다면, Nginx를 시작해준다.  
```bash
sudo service nginx start
//또는
sudo systemctl start nginx
```  

## Nginx 실행중인지 확인  
Nginx가 잘 구동중인지 확인하려면 다음과 같이 입력하면 된다.  
```bash
sudo service nginx status
```

![nginx_start](/assets/images/nginx_start.png)     
이후, 해당 AWS의 도메인 주소를 주소창에 입력하면 페이지가 잘 열리는것을 확인할 수 있다.  

![nginx_home](/assets/images/nginx_home.png)  

## FrontEnd 배포(Vue, React)  
VSCode로 vue파일을 연 후, `pakage.json`파일에 다음을 추가한다.  
```json
"Scripts": {
  ...
  "build": "vue-cli-service build"
  ...
}
```  

그리고 터미널에 build명령어를 입력한다.  
```bash
npm run build
```  

그럼, dist폴더가 생성된 것을 확인할 수 있다.  
![dist](/assets/images/dist.png)     

이를 EC2 서버에 업로드 해주어야 하는데 나는 EC2의 /var/www/html에 위 폴더를 업로드해주었다.  
파일 전송을 위해 `FileZila`를 설치한다. 그리고 올바른 도메인주소,포트번호,키 경로 등을 설정 후 연결하여 전송해주면 된다.  
![filezila](/assets/images/filezila.png)       

이후 Nginx를 재실행해서 페이지에 접속하면 변경사항이 적용된 것을 볼 수 있다.  
```bash
sudo service nginx restart
//또는
sudo systemctl restart nginx
```  

## Backend 배포(Srping)  
이제 Spring프로젝트도 배포해주기 위해 마찬가지로 Vscode로 프로젝트를 열어준다.  
그리고 `application.properties`파일에 `server.port=7777`과 같이 포트 번호가 잘 들어가있는지 확인해준다. 
이 포트번호는 conf파일에서 설정해준 포트와 일치해야한다.   
![properties](/assets/images/properties.png)      

좌측 하단의 `Maven`에서 프로젝트 우 클릭 후 `clean`-`install`-`package`순으로 실행한다.  
만약 `Maven`탭이 보이지 않는다면 마켓플레이스에서 다음 두개의 확장프로그램을 설치해주어야 한다.  
![maveninstall](/assets/images/maveninstall.png)      

중간에 에러가 뜨는 경우 해결해주어야 다음 순서로 넘어갈 수 있다.  
나같은 경우엔 스프링에선 잡히지 않는 에러가 종종 발생해서 원인을 찾느라 애를 많이 먹었다...  

마지막까지 `BUILD_SUCCESS`가 되면 target폴더 안에 `.jar`파일일 생성된 것을 확인할 수 있다.  
![jarfile](/assets/images/jarfile.png)      

역시나 이 파일도 `FileZila`를 사용해서 아까 EC2서버에 전송한 경로로 파일을 전송해주면 된다.  
![filezila_result](/assets/images/filezila_result.png)      


## 배포 확인    
우분투로 돌아와 해당 폴더로 이동 후, jar파일을 실행한다.   
```bash
cd /var/www/html  

sudo java -jar backend-0.0.1-SNAPSHOT.jar  
```  

그럼 내부에 있던 Tomcat서버가 구동되어 백엔드 플젝이 실행되는것을 볼 수 있다.  
그리고 도메인에 접속하면 배포된 모습을 확인할 수 있다.  






