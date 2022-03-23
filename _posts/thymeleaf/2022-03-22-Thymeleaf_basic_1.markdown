---
layout : post
category : [Thymeleaf]
title : Thymeleaf의 변수 방식
tagline : "Thymeleaf"
tags : [Thymeleaf]
---
## 변수방식

- HTML

```html
<!DOCTYPE HTML>
<html>
  ...
  <p th:text="${text}"></p>
  ...
</html>
```

- Controller

```java
@RequestMapping("/")
@Controller
public class Controller {
 
  @RequestMapping("/test"){
  public String test(Model model){
    model.setAttribute("text", "test String");
    return "test";
  }
}
```

- 결과

```
test String
```

위에 setAttribute한 text값이 표시된다.
