---
layout : post
category : [Spring Security]
title : Spring Security 기본
tagline : "Spring Security"
tags : [Spring Security]
---

## 개발환경 구축

- gradle

```java
implementation 'org.springframework.boot:spring-boot-starter-security'
implementation 'org.springframework.security:spring-security-test'
```



## Config 구현

- Config

```java
@Configuration
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
	@Override
	protected void configure(HttpSecurity http) throws Exception {
		http
			.authorizeRequests()
            	 // 인증이 필요없는 url 입력 (현재 root와 home 설정됨)
				.antMatchers("/", "/home").permitAll()
				.anyRequest().authenticated()
				.and()
			.formLogin()
				.loginPage("/login")
				.permitAll()
				.and()
			.logout()
				.permitAll();
	}
}
```



- Service

```java
@Bean
@Override
public UserDetailsService userDetailsService() {
	UserDetails user =
		 User.withDefaultPasswordEncoder()
			.username("user")
			.password("password")
			.roles("USER")
			.build();
	return new InMemoryUserDetailsManager(user);
}
```