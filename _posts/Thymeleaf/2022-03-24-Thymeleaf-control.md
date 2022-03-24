---
layout : post
category : [Thymeleaf]
title : Thymeleaf 제어문
tagline : "Thymeleaf"
tags : [Thymeleaf]
---

## 변수식

- HTML
```html
<!DOCTYPE HTML>
<html>
    ...
	<p th:text="${condition} ? ${trueValue} : ${falseValue}"></p>
    ...
</html>
```

- Controller
```java
@Controller
public class Controller{
	@RequestMapping("/calc")
	public ModelAndView calc(ModelAndView mav){
		mav.setViewName("calc");
		
		mav.addObject("condition", "true");
		mav.addObject("trueValue", "0");
		mav.addObject("falseValue", "9999");
		
		return mav;
	}
}
```

- 결과
```
0
```



## if문
```html
<!DOCTYPE HTML>
<html>
    ...
	<p th:if="${condition}" th:text="${trueValue}"></p>
	<p th:unless="${condition}" th:text="${falseValue}"></p>
    ...
</html>
```

- 결과
```
0
```



## switch문

```html
<!DOCTYPE HTML>
<html>
    ...
	<div th:switch="${number}">
		<p th:case="1" th:text="11">1</p>
		<p th:case="2" th:text="22">2</p>
		<p th:case="3" th:text="33">3</p>
		<p th:case="*">x</p>
	</div>
    ...
</html>
```

- Controller
```java
@Controller
public class Controller{
	@RequestMapping("/{number}")
	public ModelAndView calc(@PathVariable int number, ModelAndView mav){
		mav.setViewName("index");
	
		mav.addObject("number", number);
		return mav;
	}
}
```

- 결과 (2 입력)
```
22
```

- 결과 (5 입력)
```
x
```



## 반복문
```html
<!DOCTYPE HTML>
<html>
    ...
	<table border="1">
        <tr>
            <td>Name</td>
            <td>Nickname</td>
        </tr>
        <tr th:each="obj:${list}">
        	<td th:text="${obj[0]}"></td>
            <td th:text="${obj[1]}"></td>
        </tr>
    </table>
    ...
</html>
```

- Controller
```java
@Controller
public class Controller{
	@RequestMapping("/{user_info}")
	public ModelAndView calc(ModelAndView mav){
		mav.setViewName("user_info");
	
		ArrayList<String[]> list = new ArrayList<String[]>();
		list.add(new String[] {"ByeongDong", "BD"});
		list.add(new String[] {"JaeYong", "Observer"});
		
		mav.addObject("list", list);
		return mav;
	}
}
```

- 결과
```
-------------------------
| Name       | Nickname |
| ---------- | -------- |
| ByeongDong | BD       |
|------------|----------|
| JaeYong    | Observer |
-------------------------
```