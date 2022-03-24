---
layout : post
category : [Spring Security]
title : Spring Security에 JPA 연동
tagline : "Spring Security"
tages : [Spring Security]
---

## JPA 연동

- Entity
```java
@Entity
public class Account {
    
    @Id
    @GeneratedValue
    private Long id;
    
    @Column(unique = true)
    private String username;
    
    private String password;
    
    private String role;
    
    public void encodePassword(Encryptor encryptor){
        this.password = encryptor.encode(this.password);
    }
}
```



- Service

```java
@Service
@RequiredArgsConstructor
public class AccountService implements UserDetailService {
    
    private final AccountRepository accountRepository;
    private final Encryptor encryptor; // Bean으로 등록되어 BCryptEncryptor 호출
    
    @Override
    public UserDetails loadUserByUsername(String username) throws Exception{
        final Account account = accountRepository.findByUsername(username);
        return Optional.ofNullable(account).map(userAccount::new)
            .orElseThrow(() -> new Exception(username)); // Exception 보통 정의하여 사용
    }
    
    @Transactional
    Public Account createNew(Account account){
        account.encodePassword(passwordEncoder);
        return accoutnRepository.save(account);
    }
    
    @Transactional
    public Optional<User> findPwMatchUser(Account account) {
        return accoutnRepository.findByUsername(account.username)
                .map(u -> u.isMatched(encryptor, userPw) ? u : null);
    }
}
```



- Repository

```java
@Repository
public interface AccountRepository extends JpaRepository<Account, Long> {
    Optional<Account> findByUsername(String username);
}
```