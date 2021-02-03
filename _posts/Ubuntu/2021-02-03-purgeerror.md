---
title:  "[Ubuntu] MYSQL이 purge가 안될때 해결법"
permalink: /categories/ubuntu/purgeerror
author_profile: true
categories:
  - Ubuntu
tags:
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2021-02-03
toc: true
toc_sticky: true
---

우분투에서 설치된 MySQL를 삭제하기 위해서  
`sudo dpkg --get-selections | grep mysql`을 입력한 후 설치된 목록을 확인했다.
![20210203_224534](/assets/images/20210203_224534.png)  
여기서 `dpkg --purge mysql-client-core-8.0`로 삭제하면 다음과 같이 에러가 발생했다.
```

```