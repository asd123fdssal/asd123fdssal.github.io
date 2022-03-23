---
layout : post
category : [Thymeleaf]
title : Thymeleaf 기초
tagline : "Thymeleaf"
tags : [Thymeleaf]
---
# Thymeleaf란?


- 컨트롤러가 전달한 값을 동적으로 표시하기 위한 뷰 템플릿 (View Template)

# Dependency 추가


```java
implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
```

# Thymeleaf의 기본형


Thymeleaf의 사용법에는 4가지가 있다.


- 변수 방식 
  * ${}
- 메세지 방식
  * #{}
- 객체 변수 방식
  * *{}
- 링크 방식
  * @{}
