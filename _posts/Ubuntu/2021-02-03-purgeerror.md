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
Failed to start mysqld.service: Unit mysqld.service not found
```


이 에러를 해결하기 위해서 열심히 구글링한 결과 아래와 같이 차례대로 입력해주면 된다.  
```
sudo apt-get install --reinstall mysql-server-8.0

ls -laF /lib/systemd/system/mysql.service

sudo apt-get install -f
sudo dpkg --configure -a

sudo killall mysqld
sudo systemctl disable mysql.service
sudo rm -rf /lib/systemd/system/mysql.service
sudo rm -rf /usr/lib/systemd/system/mysql.service
sudo rm -rf /etc/systemd/system/multi-user.target.wants/mysql.service
sudo rm -rf /var/lib/systemd/deb-systemd-helper-enabled/multi-user.target.wants/mysql.service
sudo rm -rf /var/cache/apt/archives/mysql-server-*.deb

sudo apt-get install -f
sudo dpkg --configure -a

sudo apt-get install --reinstall mysql-server-8.0
```  

그리고 다시 `dpkg --purge mysql-client-core-8.0`를 입력해주면 정상적으로 삭제 처리가 된다.  