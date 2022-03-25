---
layout : post
category : [정보처리기사,디자인패턴]
title : Abstract Factory 패턴
tagline : "정보처리기사,디자인패턴"
tags : [정보처리기사,디자인패턴]
date : "2022-03-25 13:45:00"
---

구체적인 클래스에 의존하지 않고 연관, 의존적인 객체의 조합을 만드는 인터페이스를 제공

구체적인 구현은 Concrete Product 클래스에서 이루어짐

동일 주제의 다른 팩토리를 묶는다.



## 클래스 다이어그램 [^출처]



<img style="Background-color:white" src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/Abstract_factory.svg/600px-Abstract_factory.svg.png" alt="Abstract factory.svg">



## 소스코드

```java
public interface IButton {
    void Paint();
}
```

```java
public interface IGUIFactory {
    IBtton CreateButton();
}
```

```java
public class WinButton extends IButton {
    public void Paint() {
        // Paint the button Windows style
    }
}
```

```java
public class OSXButton extends IButton {
    public void Paint() {
        // Paint the button OSX style
    }
}
```

```java
public class WinFactory implements IGUIFactory {
    @Override
    protected IButton CreateButton() {
        return new WinButton();
    }
}
```

```java
public class OSXFactory implements IGUIFactory {
    @Override
    protected IButton CreateButton() {
        return new OSXButton();
    }
}
```

```java
public class AbsFactoryExample {
    public static void main(String args[]) {
        String style = DesignConfig.STYLE;
        
        IGUIFactory factory;
        if(style == FormStyle.WIN){
            factory = new WinFactory();
        }else if(style == FormStyle.OSX){
            factory = new OSXFactory();
        }else{
            throws new NotImplementedException();
        }
        
        Button button = factory.CreateButton();
        button.paint();
    }
}
```



[^출처]: https://ko.wikipedia.org/wiki/%EC%B6%94%EC%83%81_%ED%8C%A9%ED%86%A0%EB%A6%AC_%ED%8C%A8%ED%84%B4