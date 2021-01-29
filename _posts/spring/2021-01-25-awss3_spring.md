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

이번 프로젝트를 진행하면서 AWS S3를 이미지 업로드 서버로 사용하여 로컬과 따로 분리하여 관리할 수 있도록 해주었다.  
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
   

## 3. 스프링에서 연동하기  
1) pom.xml 설정  
pom.xml에 아래 라이브러리들을 넣어준다.  
```xml
<!-- https://mvnrepository.com/artifact/com.amazonaws/aws-java-sdk-s3 -->
		<dependency>
			<groupId>com.amazonaws</groupId>
			<artifactId>aws-java-sdk-s3</artifactId>
			<version>1.11.942</version>
		</dependency>


		<!-- https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-starter-aws -->
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-aws</artifactId>
			<version>2.2.5.RELEASE</version>
		</dependency>

		<!-- https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-aws -->
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-aws</artifactId>
			<version>2.2.1.RELEASE</version>
			<type>pom</type>
		</dependency>
```
  
2) 스프링 프로젝트의 `aplication.properties`에 발급받은 키 정보를 적어준다.  
```java
# Google Email Server
cloud.aws.credentials.accessKey=인증키
cloud.aws.credentials.secretKey=보안키
cloud.aws.s3.bucket=artmatebucket
cloud.aws.region.static=ap-northeast-2
cloud.aws.stack.auto=false
```  



3) @Configuration 클래스 생성   
`WebMvcConfig`클래스는 기본적인 서블릿 설정을 하는 클래스이다.  


```java
package com.ssafy.artmate.aws;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

import com.amazonaws.auth.AWSStaticCredentialsProvider;
import com.amazonaws.auth.BasicAWSCredentials;
import com.amazonaws.regions.Regions;
import com.amazonaws.services.s3.AmazonS3;
import com.amazonaws.services.s3.AmazonS3ClientBuilder;

@Configuration
@EnableWebMvc
public class AWSConfiguration implements WebMvcConfigurer {
	
	@Value("${cloud.aws.credentials.accessKey}")
	private String accessKey;
	
	@Value("${cloud.aws.credentials.secretKey}")
	private String secretKey;
	
	
	@Bean
	public BasicAWSCredentials AwsCredentials() {
		BasicAWSCredentials AwsCreds = new BasicAWSCredentials(accessKey, secretKey);	
		return AwsCreds;
	}	
	
	@Bean
	public AmazonS3 AwsS3Client() {
		
		AmazonS3 s3Builder = AmazonS3ClientBuilder.standard()
				.withRegion(Regions.AP_NORTHEAST_2)
				.withCredentials(new AWSStaticCredentialsProvider(this.AwsCredentials()))
				.build();	

		return s3Builder;
	}
}
```  

4) AwsS3Service    
S3서버에 파일 전송, 가져오기, 삭제등을 하는 서비스 클래스를 생성한다.  

```java
package com.ssafy.artmate.service;

import java.io.IOException;
import java.net.URL;
import java.text.SimpleDateFormat;
import java.util.Date;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.core.io.ByteArrayResource;
import org.springframework.core.io.Resource;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;
import org.springframework.web.multipart.MultipartFile;

import com.amazonaws.AmazonServiceException;
import com.amazonaws.services.s3.AmazonS3;
import com.amazonaws.services.s3.AmazonS3Client;
import com.amazonaws.services.s3.model.DeleteObjectRequest;
import com.amazonaws.services.s3.model.GetObjectRequest;
import com.amazonaws.services.s3.model.ObjectMetadata;
import com.amazonaws.services.s3.model.PutObjectRequest;
import com.amazonaws.services.s3.model.S3Object;
import com.amazonaws.services.s3.model.S3ObjectInputStream;
import com.amazonaws.util.IOUtils;

import lombok.extern.slf4j.Slf4j;

@Slf4j
@Service
@Transactional(rollbackFor = Exception.class)
public class AwsS3Service {

	@Autowired
	private AmazonS3Client AwsS3Client;
	
	@Value("${cloud.aws.credentials.accessKey}")
	private String accessKey;

	@Value("${cloud.aws.s3.bucket}")
	private String bucketName;
	
	@Value("${cloud.aws.region.static}")
	private String region;

	public String uploadObject(MultipartFile multipartFile, String storedFileName, String folder) throws IOException {
		SimpleDateFormat date = new SimpleDateFormat("yyyyMMdd");
		ObjectMetadata omd = new ObjectMetadata();
		omd.setContentType(multipartFile.getContentType());
		omd.setContentLength(multipartFile.getSize());
		omd.setHeader("filename", multipartFile.getOriginalFilename());

		// Copy file to the target location (Replacing existing file with the same name)
		int random = (int) Math.floor(Math.random()*9999);
		
		AwsS3Client.putObject(new PutObjectRequest(bucketName+"/"+folder, random+storedFileName,
				multipartFile.getInputStream(), omd));
		
        storedFileName; //이미지 url 리턴
		return AwsS3Client.getResourceUrl(bucketName, folder+"/"+random+storedFileName); //서버에 저장된 이미지 url 리턴
		
	}

	public void deleteObject(String url, String folder) throws AmazonServiceException {
		String totalFileName = url.substring(url.indexOf(folder+"/"));
		System.out.println(totalFileName);
		AwsS3Client.deleteObject(new DeleteObjectRequest(bucketName, totalFileName));
	}

	public Resource getObject(String date, String storedFileName) throws IOException {
		S3Object o = AwsS3Client.getObject(new GetObjectRequest(bucketName + "/" + date, storedFileName));
		S3ObjectInputStream objectInputStream = o.getObjectContent();
		byte[] bytes = IOUtils.toByteArray(objectInputStream);
		
		Resource resource = new ByteArrayResource(bytes);
		return resource;
	}
	
}
```  


5) Controller 생성    
파일을 업로드를 하기 위한 Controller를 생성해서 aws서비스 객체를 사용해 s3로 이미지파일을 전송해주면 된다.  

```java
String url = awservice.uploadObject(file, file.getOriginalFilename(), "feed");
```  

다음과 같이 실제 s3에도 업로드 된 것을 볼 수 있다.  
![awss3_result](/assets/images/awss3_result.png) 