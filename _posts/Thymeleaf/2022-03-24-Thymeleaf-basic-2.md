---
layout : post
category : [Thymeleaf]
title : Thymeleaf의 메세지 방식
tagline : "Thymeleaf"
tags : [Thymeleaf]
---

## 메세지 방식

- properties

```properties
dev.version=1.0.0
```

- HTML

```html
<!DOCTYPE HTML>
<html>
  ...
  <p th:text="Version is #{dev.version}"></p>
  ...
</html>
```

  - 결과

```
Version is 1.0.0
```

​    