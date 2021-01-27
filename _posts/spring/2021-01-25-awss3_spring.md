---
title:  "[Spring] Spring Boot에서 AWS S3 파일 업로드,다운받기"
excerpt: "Spring에서 AWS S3연동, 사용법"
permalink: /categories/spring/awss3_spring
author_profile: true
categories:
  - Spring
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2021-01-25
toc: true
toc_sticky: true
---


# AWS S3란?
> Simple Storage Service의 약자.
> 인터넷상 어디서나 원하는 양의 데이터를 저장하고 검색할 수 있도록 구축된 서비스  

## 특징
* 많은 사용자가 접속해도 이를 감당하기 위한 시스템적인 작업을 하지 않아도 된다.  
* 저장할 수 있는 파일 수의 제한이 없다.
* 최소 1바이트에서 최대 5TB의 데이터를 저장하고 서비스할 수 있다.
* REST, SOAP 인터페이스를 제공한다.   

나는 이번 프로젝트에서 AWS S3를 이미지 업로드 서버로 사용하여 로컬과 따로 분리하여 관리할 수 있도록 해주었다.  
AWS S3는 AWS 회원가입 후 프리티어로 5GB까지 무료로 이용할 수 있다(GET요청 20000번, POST요청 2000번까지) 
[가입하러 가기](https://aws.amazon.com/ko/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Categories=categories%23storage&trk=ps_a134p000006gGiOAAU&trkCampaign=acq_paid_search_brand&sc_channel=PS&sc_campaign=acquisition_KR&sc_publisher=Google&sc_category=Storage&sc_country=KR&sc_geo=APAC&sc_outcome=acq&sc_detail=aws%20s3&sc_content=S3_e&sc_matchtype=e&sc_segment=477202843563&sc_medium=ACQ-P|PS-GO|Brand|Desktop|SU|Storage|S3|KR|EN|Text&s_kwcid=AL!4422!3!477202843563!e!!g!!aws%20s3&ef_id=CjwKCAiAu8SABhAxEiwAsodSZMXf_E7yfRJlQ9nZjt_KN0hHpvBSWojZaiwyCmC9RJxJk9PJpoGIExoCY08QAvD_BwE:G:s&s_kwcid=AL!4422!3!477202843563!e!!g!!aws%20s3)
![awss3_1](/assets/images/awss3_1.png)      

## 1. 버킷만들기
[여기서](https://s3.console.aws.amazon.com/s3/home?region=ap-northeast-2) 버킷을 만들어준다.  
버킷이름은 예를 들어 '프로젝트+bucket'으로 지을 수 있다.  
버킷 생성 후, '권한'-'버킷 정책'에서 정책을 설정한다.  
![awss3_2](/assets/images/awss3_2.png)  
```
{
    "Version": "2012-10-17",
    "Id": "Policy1577077078140",
    "Statement": [
        {
            "Sid": "Stmt1577076944244",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::artmatebucket/*"
        }
    ]
}
```

## 2. ACCESS KEY 발급  
우측 상단 탭의 '내 아이디'-'보안 자격 증명'에서 ACCESS KEY를 발급해준다.  
이때, Access Key와 보안 Access Key를 잘 기억해준다.   
![awss3_3](/assets/images/awss3_3.png)    

