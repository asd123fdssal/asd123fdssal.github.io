---
layout : post
category : [Spring Security]
title : Spring Security 패스워드 암호화
tagline : "Spring Security"
tages : [Spring Security]
---

## 패스워드 암호화

- Encryptor
```java
public interface Encryptor {
	String encrypt(String origin);
	boolean isMatch(String origin, String hashed);
}
```



- BCryptEncryptor

```java
public class BCryptEncryptor implements Encryptor {
	@Override
	public String encrypt(String origin) {
		return BCrypt.hashpw(origin, BCrypt.gensalt());
	}
	
	@Override
	public boolean isMatch(String origin, String hashed) {
		try {
			return BCrypt.checkpw(origin, hashed);
		} catch (Exception e) {
			return false;
		}
	}
}
```



- WebSecurityConfig

```java
public class WebSecurityConfig {
// Bean으로 등록 시 @Autowired를 통해 Encryptor 선언 시 자동으로 클래스 바인딩
	@Bean 
    public Encryptor encryptor(){
        return new BCryptEncryptor();
    }
}
```