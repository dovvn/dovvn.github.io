---
title:  "[Nginx] Nginx에서 HTTPS/SSL 적용하기 "
permalink: /categories/spring/nginx_htps
author_profile: true
categories:
  - Spring
tags:
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2021-02-11
toc: true
toc_sticky: true
---  

사이트에 https를 적용해야 하는 이유?  
웹사이트를 https로 전환해야 하는 이유에는 여러가지가 있다.  
구글, 파이어폭스부터 브라우저를 https로 전환하고 있는데 그 이유가 무엇일까?   
https를 사용하게 되면 서버와 브라우저 사이에 암호화 연결을 만들수 있고 민감한 정보를 받을때 도난당하는 것을 막아준다.  
다음과 같이 nginx를 활용해 ssl인증서를 발급받는 법은 다음과 같다.   

기존의 http에서 listen후 htpps로 보내주기 위해서 https 포트번호로 돌려주는 리다이렉트 과정이 필요하다.  
깃 clone후 프로젝트 경로에서 다음과 같이 letsencrypt로 이동해 무료로 SSL인증서를 발급한다.  

```bash
$ ./letsencrypt-auto --help
```

설치 후, 다음과 같이 입력한다. 
```bash
./letsencrypt-auto certonly --standalone -d YOUR_DOMAIN
```  

그리고 nginx 세팅을 위해 필요한 인증서 위치를 저장해둔다.  
```bash
/etc/letsencrypt/live/[YOUR DOMAIN]/fullchain.pem
/etc/letsencrypt/live/[YOUR DOMAIN]/privkey.pem
```  

letsencrypt로 받은 인증서를 아래와 같이 새로 세팅한다.   
```  
vi /etc/nginx/nginx.conf  
worker_processes  1;

events {
    worker_connections  1024;
}
http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;

    server {
        listen       80;
        server_name [YOUR_DOMAIN];
        client_max_body_size 30M;
        keepalive_timeout 5;
        return 301 https://$server_name$request_uri;

    }
    # HTTPS server
    server {
        listen       443 default_server ssl;
        server_name  [YOUR DOMMAIN];

        ssl_certificate      [YOUR_SSL_CERTIFICATE_LOCATION];
        ssl_certificate_key  [YOUR_SSL_CERTIFICATE_KEY_LOCATION];
        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;

        location / {
             proxy_set_header X-Forwarded-For 		  $proxy_add_x_forwarded_for;
             proxy_set_header X-Forwarded-Proto https;
             proxy_set_header X-Real-IP $remote_addr;
             proxy_set_header HOST $http_host;
             proxy_set_header X-NginX-Proxy true;

             proxy_pass http://127.0.0.1:[YOUR PORT];
             proxy_redirect off;
        }
    }
}
```  
 letsencrypty에서 발급후 저장을 완료했다면 service nginx restart를 입력해서 재시작해준다.  


 ### 참고
 - [SSL 인증서 설치 메뉴얼](https://cert.crosscert.com/nginx-ssl%EC%9D%B8%EC%A6%9D%EC%84%9C-%EC%84%A4%EC%B9%98-%EB%A7%A4%EB%89%B4%EC%96%BC/)  
 - [Nginx HTTPS 및 Let's Encryt SSL 인증서 적용](https://jackerlab.com/nginx-https-lets-encrypt/)  
 - https://help.campaignus.me/article/96-change-social-api-protocol
 - https://taewooblog.tistory.com/142