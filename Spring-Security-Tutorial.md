---
title: Spring Security Tutorial
date: 2021-05-25 09:29:56
tags:
categories:
---

创建项目时导入相关依赖，会有默认的http认证界面

#### 禁用默认Security登录

找到Spring Boot启动类

```java
@EnableAutoConfiguration(exclude = {SecurityAutoConfiguration.class})
```



[数据库demo](https://blog.csdn.net/qq_43647821/article/details/111628821)

---

#### 密码有问题

密码的编码问题

解决

Add password storage format

```java
@Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
     
        auth.inMemoryAuthentication()
                .withUser("user").password("{noop}password").roles("USER")
                .and()
                .withUser("admin").password("{noop}password").roles("ADMIN");

    }
```



---

#### Spring Security 配置数据库验证用户登录

[Demo](https://github.com/a1020151695/Spring-Security-DEMO)

1.Security 过滤链

继承WebSecurityConfigurerAdapter 重写其中的configure进行配置

总共3种configure可重写

1.HttpSecurity， 配置路由

```java
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.csrf().disable();
        http.apply(new JLoginConfigurer<>());
        http.authorizeRequests()
                .antMatchers("/user/login_frontend").permitAll()
                .anyRequest()
                .hasAuthority("USER").and()
                .formLogin()
                .loginPage("/user/login_frontend")
                .defaultSuccessUrl("http://localhost:8081/?state=user",true);
    }
```

2.AuthenticationManagerBuilder， 配置认证

```java
    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
//        auth.inMemoryAuthentication().withUser("user").password(passwordEncoder.encode("123456")).roles("USER").authorities("USER");  
//        auth.inMemoryAuthentication().withUser("user1").password(passwordEncoder.encode("123456")).roles("USER").authorities("USER");
          auth.userDetailsService(userService);
          auth.jdbcAuthentication().passwordEncoder(passwordEncoder).rolePrefix("");
    }
```

3.WebSecurity， 配置静态资源的访问

```java
        @Override
        public void configure(WebSecurity web) throws Exception {
            // static resource
            web.ignoring().antMatchers("/css/**", "/img/**", "/**/*.png"); // 忽略对这些请求的拦截
        }
```



重点在对于认证的configure

其中另外涉及到了两个东西

UserService，PasswordEncoder

UserService实现UserDetailsService接口，实现loadUserByUsername方法

```java
package freejim.icu.security_demo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.stereotype.Service;

@Service
public class UserService implements UserDetailsService {
    @Autowired
    UserRepository userRepository;

    @Autowired
    PasswordEncoder passwordEncoder;

    public User insert(User user) {
        //存在数据库中的密码应该为密文
        // 不可少！不然密码编码错误，会导致正确的密码也无法登录
        user.setPassword(passwordEncoder.encode(user.getPassword())); 
        return userRepository.save(user);
    }

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



PasswordEncoder

```java
package freejim.icu.security_demo;

import org.springframework.context.annotation.Bean;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.stereotype.Component;

@Component  // 自动装配
public class PasswordUtil {
    @Bean
    PasswordEncoder passwordEncoder(){
        return new BCryptPasswordEncoder();
    }
}

```

上面又涉及到和数据库的交互

即UserRepository 和User

UserRepository 完成与数据库的交互

```java
package freejim.icu.security_demo;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository  // 注解实现，依赖于jpa
public interface UserRepository extends JpaRepository<User,Long> {
    User findByName(String name);
}

```

User 其实不只是实体类那么简单，其实现了很重要的UserDetails接口

UserDetails 是在认证过程中负责用户信息储存的接口

```java
package freejim.icu.security_demo;

import lombok.Data;

import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.authority.SimpleGrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import java.util.ArrayList;
import java.util.Collection;
import java.util.List;

@Entity(name = "tb_user")  // tb_user 为表名
@Data
public class User implements UserDetails {

    @Id //标识为主键
    @GeneratedValue(strategy = GenerationType.IDENTITY)  //主键自增
    private Long id;
    private String name;
    private String password;
    private String role;


    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        List<SimpleGrantedAuthority> simpleGrantedAuthorities = new ArrayList<>();
        simpleGrantedAuthorities.add(new SimpleGrantedAuthority("role"));
        return simpleGrantedAuthorities;
    }

    @Override
    public String getPassword() {
        return password;
    }

    @Override
    public String getUsername() {
        return name;
    }

    @Override
    public boolean isAccountNonExpired() {
        return true;
    }

    @Override
    public boolean isAccountNonLocked() {
        return true;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        return true;
    }

    @Override
    public boolean isEnabled() {
        return true;
    }
}

```

然后是数据库的配置

application.properties

```
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/db_authority?serverTimezone=GMT%2B8
spring.datasource.username=root
spring.datasource.password=123456
```

mysql语句

```sql
CREATE TABLE `tb_user` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL COMMENT '用户名',
  `password` varchar(255) DEFAULT NULL COMMENT '用户密码',
  `role` varchar(255) DEFAULT NULL COMMENT '用户角色，所拥有的权限',
  PRIMARY KEY (`id`)
);
```

配置完成

---

认证后只通过Cookie

hasRole is the Key

---

#### Spring Security 定制认证

整合vue

```java
        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http.authorizeRequests()
                    .antMatchers("/user/**")  // 匹配所有请求
                    .hasAnyRole("USER").and()
                    .formLogin()
                    .loginPage("http://localhost:8081/loginpage").permitAll()  // 自定义登录页面
                    .loginProcessingUrl("/auth")
           .defaultSuccessUrl("http://localhost:8081/").and()  // 配置登陆成功后的跳转页面
                    .logout()
                    .logoutUrl("/user/logout")
                    .logoutSuccessUrl("/user/login_frontend?logout");
            http.csrf().disable();
        }
```

---

#### defaultSuccessUrl

通过表单登录的走这个

而且注意，其分为继续访问和指定访问模式

```java
.defaultSuccessUrl("http://localhost:8081/?state=user",true);
```

true 为alwaysUse

---



