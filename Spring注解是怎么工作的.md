---
title: Spring注解是怎么工作的
date: 2020-11-05 17:05:39
tags:
- Spring
- Java
categories:
- [Java,Spring]
---

版本说明：Spring 5.2.9 

本文侧重于源码的解读

这里以@Autowired为例

```java
public class AutowiredAnnotationBeanPostProcessor
extends Object
implements SmartInstantiationAwareBeanPostProcessor, MergedBeanDefinitionPostProcessor, PriorityOrdered, BeanFactoryAware
```

[`BeanPostProcessor`](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/config/BeanPostProcessor.html) implementation that autowires annotated fields, setter methods, and arbitrary config methods. Such members to be injected are detected through annotations: by default, Spring's [`@Autowired`](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/annotation/Autowired.html) and [`@Value`](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/annotation/Value.html) annotations.

```java
public void processInjection(Object bean) throws BeanCreationException {
		Class<?> clazz = bean.getClass();
		InjectionMetadata metadata = findAutowiringMetadata(clazz.getName(), clazz, null);
		try {
			metadata.inject(bean, null, null);
		}
		catch (BeanCreationException ex) {
			throw ex;
		}
		catch (Throwable ex) {
			throw new BeanCreationException(
					"Injection of autowired dependencies failed for class [" + clazz + "]", ex);
		}
	}
```



获取AutowiringMetadata后，做inject

其中的AutowiringMetadata，简单的说就是@Autowired

> an **annotation** is a form of syntactic [metadata](https://en.wikipedia.org/wiki/Metadata) that can be added to Java [source code](https://en.wikipedia.org/wiki/Source_code).

这是维基百科上的解释

那Spring又是怎么确定是否存在@Autowired的呢

```java
	private MergedAnnotation<?> findAutowiredAnnotation(AccessibleObject ao) {
		MergedAnnotations annotations = MergedAnnotations.from(ao);
		for (Class<? extends Annotation> type : this.autowiredAnnotationTypes) {
			MergedAnnotation<?> annotation = annotations.get(type);
			if (annotation.isPresent()) {
				return annotation;
			}
		}
		return null;
	}
```

其中的

```java
private final Set<Class<? extends Annotation>> autowiredAnnotationTypes = new LinkedHashSet<>(4);

this.autowiredAnnotationTypes
```

```java
public AutowiredAnnotationBeanPostProcessor() {
		this.autowiredAnnotationTypes.add(Autowired.class);
		this.autowiredAnnotationTypes.add(Value.class);
		try {
			this.autowiredAnnotationTypes.add((Class<? extends Annotation>)
					ClassUtils.forName("javax.inject.Inject", AutowiredAnnotationBeanPostProcessor.class.getClassLoader()));
			logger.trace("JSR-330 'javax.inject.Inject' annotation found and supported for autowiring");
		}
		catch (ClassNotFoundException ex) {
			// JSR-330 API not available - simply skip.
		}
	}
```



已经很清晰了，存放了Autowired.class

则回到findAutowiredAnnotation()中，如果

```java
MergedAnnotations annotations = MergedAnnotations.from(ao);
```

```java
public interface MergedAnnotations
extends Iterable<MergedAnnotation<Annotation>>
```

Provides access to a collection of merged annotations, usually obtained from a source such as a [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html?is-external=true) or [`Method`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html?is-external=true).

获取这个Bean 的Annotations

然后看其中是否存在Autowired

那么确定是否有Autowired的问题解决了，之后就是inject了

---

首先来看看调用inject()的InjectionMetadata

```java
public class InjectionMetadata
extends Object
```

Internal class for managing injection metadata. Not intended for direct use in applications.

对的，这个就是依赖注入里的inject

不过，我暂时没有想法去了解，有兴趣的同学可以继续往下了解



---



[Field](http://www.avajava.com/tutorials/lessons/how-do-i-list-the-declared-fields-of-a-class.html)