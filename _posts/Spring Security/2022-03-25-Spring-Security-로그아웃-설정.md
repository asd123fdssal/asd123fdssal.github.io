---
layout : post
category : [Spring Security]
title : Spring Security 로그아웃 Filter
tagline : "Spring Security"
tags : [Spring Security]
---

## 로그아웃 Filter

```java
@Configuration
@EnableWebSecurity
@RequiredArgsConstructor
public class SecurityConfig extends WebSecurityConfiguraterAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.logout()
            .logoutUrl("/logout")
            .logoutSuccessUrl("/")
            .logoutRequestMatcher(new AntPathRequestMatcher("/logout"))
            .invalidateHttpSession(true) 
            .deleteCookies("SESSION_ID") 
            .addLogoutHandler(handler) 
            .logoutSuccessHandler(handler);
    }
}
```

