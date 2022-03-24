---
layout : post
category : [Spring Security]
title : 로그인 Controller 구현
tagline : "Spring Security"
tags : [Spring Security]
---

## Controller 구현

- Account DTO 구현
```java
@Getter
@Setter
@NoArgsConstructor
@Builder
public class AccountDto {
    private Long id;
    private String username;
    private String password;
    
    public Account toEntity() {
        return Account.builder()
            .id(id)
            .username(username)
            .password(password)
            .build;
    }
}
```

```java
@Controller
@AllArgsConstructor
public class AccountController {
    private AccountService accountService;
    
    public static String SESSION_ID = "SESSION_ID"
    
    @GetMapping("/")
    public String index(){
        return "index";
    }
    
    @GetMapping("/signup")
    public String signup(Model model){
        model.addAttribute("account", new AccountDto());
        
        return "/signup"
    }
    
    @PostMapping("/signup")
    public String signup(AccountDto accountDto) {
        AccountService.signUp(accountDto);
        
        return "redirect:/";
    }
    
    @GetMapping("/login")
    public String login() {
        return "/loginForm";
    }
    
    @PostMapping("/login")
    public String login(@ModelAttribute @Validated LoginForm loginForm,
                       BindingResult bindingResult
                       @RequestParam(defaultValue = "/") String redirectURL) {
        if (bindingResult.hasErrors()){
            return "/loginForm";
        }
        
        Account account = AccountService.login(loginForm.getUsername(), loginForm.getPassword());
        if (account == null){
            bindingResult.reject("loginFailed", "아이디 또는 비밀번호가 일치하지 않습니다.");
            return "/loginForm";
        }
        
        HttpSession session = request.getSession();
        session.setAttribute(SESSION_ID, account);
        
        return "redirect:" + redirectURL;
    }
    
    @PostMapping("/logout")
    public String logout(HttpServletRequest request) {
        HttpSession session = request.getSession(false);
        
        if(session != null) {
            session.invalidate();
        }
        
        return "redirect:/";
    }
}
```

