---
layout : post
category : [Thymeleaf]
title : Thymeleaf 링크 방식
tagline : "Thymeleaf"
tags : [Thymeleaf]
---

## 링크 방식

- HTML
```html
<!DOCTYPE HTML>
<html>
    ...
	<a th:href="@{'/game/list'}">Go to game list</a>
    ...
</html>
```

- 결과
<u>Go to game list</u>

Link 클릭 시
```
https://Base_URL/game/list로 이동
```