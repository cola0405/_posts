---
title: 汇编-Spring重构
date: 2020-11-05 21:23:17
tags:
- Spring
categories:
- [Java,Spring]
---

1.javax 是由Tomcat提供的

2.Context 养成好习惯，用完记得close()

3.“一次性”的变量能省就省

```java
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		WebApplicationContext context=WebApplicationContextUtils.getWebApplicationContext(request.getServletContext());
		context.getBean("helloImpl",Hello.class).sayHello();
	}
```



4.Spring DI Bean之间是由依赖关系的，被引用的那个Bean应该先被创建

XML的构建是按从上到下顺序的



5.Static Factory 方法获取Bean

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-2.0.xsd">

<bean id="bean1" class="com.dgut.factory.StaticFactory" factory-method="createBean" ></bean>
<!-- you can set properties here  -->
<!-- you can also set constructor-arg here  -->
</beans>
```

```java
package com.dgut.factory;
public class StaticFactory {
	public static MyBean createBean() {
		return new MyBean("Alice",15);
	}
}

```

```java
	void testStaticFactory() {//static 
		ConfigurableApplicationContext context =new ClassPathXmlApplicationContext("StaticFactory.xml");
		System.out.print(context.getBean("bean1",MyBean.class));
		context.close();
	}
```

只要beans.xsd

7.BeanFactory 方法获取Bean



```java
package com.dgut.factory;
public class FactoryBean {
	public MyBean createBean() {
		return new MyBean();
	}
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-2.0.xsd">

<!-- factory instance to get bean -->
<bean id="BeanFactory1" class="com.dgut.factory.FactoryBean"></bean>
<bean id="bean1" factory-bean="BeanFactory1" factory-method="createBean"></bean>
</beans>
```

只要beans.xsd

8.由方法返回的像context这样的对象是会自动close()的

也就是说，可立即使用，但不能二次使用

9.在XML中的properties---对应的是getter和setter

构造函数另有constructor-arg

但特殊情况下，properties可以代替constructor-arg，不写constructor-arg

原因是缺省constructor-arg时调用不含参的构造函数

10.当prototype和singleton都指向同一个类时

prototype 就没有意义了

11.singleton的意义是在容启启动之初检查Bean是否有问题，很有必要

所有，Bean 的默认加载方式是singleton

12.XML中的autowire

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    
<bean id="Jim" class="com.dgut.autowire.Person" autowire="byName">
<property name="name" value="Jim" ></property>
</bean>

<bean id="address" class="com.dgut.autowire.Address">
<property name="city" value="meizhou"></property>
</bean>
    
</beans>

```

```java
package com.dgut.autowire;
public class Person {
	private String name;
	Address address;
	public Person(String name, Address address) {
		super();
		this.name = name;
		this.address = address;
	}
    ...
}
----------------------------------------------------------
package com.dgut.autowire;
public class Address {
	String city;
	public Address() {
		super();
	}
	public Address(String city) {
		super();
		this.city = city;
	}
    ...
}
```

byName对应Field(也可以说property)名

byType 

>"byType" Autowiring if there is exactly one bean of the property type in the container. If there is 
>more than one, a fatal error is raised, and you cannot use byType autowiring for that bean. 





---

第一次重构就到这里啦

重构追求精简，清晰，但难免也会又进死胡同

重构完一个地方就要进行单元测试，不然到时候全部写完测出错误很麻烦

这次只展示了重构后的代码

重构前的代码。。忘记存了，下次重构不会漏了