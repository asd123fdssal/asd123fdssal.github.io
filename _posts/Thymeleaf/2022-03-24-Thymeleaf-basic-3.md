---
layout : post
category : [Thymeleaf]
title : Thymeleaf의 객체 변수 방식
tagline : "Thymeleaf"
tags : [Thymeleaf]
---

## 객체 변수 방식

- Controller
```java
@Controller
public class Controller{
	@RequestMapping("/")
	public String user_info(Model model){
		User user = new User("asd", "123")
		model.addAttribute("user_info")
		return "user_info";
	}
}
```

- DTO
```java
@RequiredArgsConstructor
public class User{
	@NotBlank
	private final String id;
	
	@NotBlank
	private final String pw;
}
```

- HTML
```html
<!DOCTYPE HTML>
<html>
    ...
	<div th:object="${user_info}">
        <p th:text="*{id}"></p>
        <p th:text="*{pw}"></p>
    </div>
    ...
</html>
```

- 결과
```
asd
123
```