---
layout : post
category : [Spring Security]
title : Spring Security 로그인 UI 구현
tagline : "Spring Security"
tags : [Spring Security,Thymeleaf]
---

## 로그인  UI 구현

- html
```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:th="https://www.thymeleaf.org"
      xmlns:sec="https://www.thymeleaf.org/thymeleaf-extras-springsecurity3">
    <head>
        <title>Spring Security 로그인 예제 </title>
    </head>
    <body>
        <div th:if="${param.error}">
            잘못된 ID 또는 비밀번호 입니다.
        </div>
        <div th:if="${param.logout}">
            로그아웃 되었습니다.
        </div>
        <-->ht:action="@{/login}"로 작성할 경우 csrf 토큰 생성이 필요 없다.</-->
        <form th:action="@{/login}" method="post">
            <div><label> 아이디 : <input type="text" name="username"/> </label></div>
            <div><label> 비밀번호: <input type="password" name="password"/> </label></div>
            <div><input type="submit" value="로그인"/></div>
        </form>
    </body>
</html>
```



## 로그인 성공 시

- html

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:th="https://www.thymeleaf.org"
      xmlns:sec="https://www.thymeleaf.org/thymeleaf-extras-springsecurity3">
    <head>
        <title>Hello World!</title>
    </head>
    <body>
        <h1 th:inline="text">Hello [[${#httpServletRequest.remoteUser}]]!</h1>
        <form th:action="@{/logout}" method="post">
            <input type="submit" value="Sign Out"/>
        </form>
    </body>
</html>
```

