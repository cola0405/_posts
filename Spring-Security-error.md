---
title: Spring Security error
date: 2021-06-12 11:29:40
tags:
categories:
---

#### Encoded password does not look like BCrypt

```java
@Autowired
PasswordEncoder passwordEncoder;
@Override
protected void configure(AuthenticationManagerBuilder auth) throws Exception {       auth.inMemoryAuthentication().withUser("user").password(passwordEncoder.encode("123456")).roles("USER").authorities("USER");
        }
```

```java
@Component
public class PasswordUtil {
    @Bean
    PasswordEncoder passwordEncoder(){
        return new BCryptPasswordEncoder();
    }

}
```



#### Spring Security 认证之后还是403

除了的csrf问题，有可能是userDetailsService没写好

```java
http.csrf().disable();
```

userDetailsService一定要把认证用户对应的权限加进去

```java
    @Override
    public UserDetails loadUserByUsername(String name) throws UsernameNotFoundException {
        User user = userRepository.findByName(name);
        System.out.println("认证中...");
        List<SimpleGrantedAuthority> authorities = new ArrayList<>();
        authorities.add(new SimpleGrantedAuthority(user.getRole()));
        if (user == null){
            System.out.println("nobody");
            return null;
        }
        return new org.springframework.security.core.userdetails.User(user.getUsername(), user.getPassword(), authorities);
    }
```

---

#### Spring Security 不起作用

只处理POST请求，GET请求无效