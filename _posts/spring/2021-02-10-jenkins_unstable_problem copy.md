---
title:  "[Jenkins] Jenkins 빌드 시 상태가 자꾸 Unstable이 뜨는 경우 Exec timed out "
permalink: /categories/spring/jenkins_unstable_problem
author_profile: true
categories:
  - Spring
tags:
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2021-02-10
toc: true
toc_sticky: true
---  

Jenkins에서 빌드수행 시 다음과 같은 에러문구가 뜨면서 상태가 Unstable으로 뜨는경우가 있다.  

```
SSH: Disconnecting configuration [batch_001] ...
ERROR: Exception when publishing, exception message [Exec timed out or was interrupted after 213,127 ms]
Build step 'Send files or execute commands over SSH' changed build result to UNSTABLE
```   

이는 설정된 시간안에 작업상황을 완료하지 못했다는 뜻으로 '구성'에 들어가서 작업 수행시간을 변경해주면 된다.  
Jenkins 프로젝트에서 '구성'-'빌드환경'에서 다음 Exec timeout을 0으로 바꾸면 무제한이라는 의미로 작업 시간에 제한을 받지 않는다.   

![jenkins_timeout](/assets/images/jenkins_timeout.png)  

이후 다시 빌드하면 timeout에러는 해결이 된다.  