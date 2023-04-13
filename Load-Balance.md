---
title: Load Balance
date: 2021-04-26 21:18:25
tags: Spring-Boot
categories:
---

[Tutorial](https://spring.io/guides/gs/spring-cloud-loadbalancer/)

1. New two project

   ```
   say-hello   // real-service
   ```

   ```
   user   // balance-server
   ```

   with maven

   ```
   say-hello need modules: Spring Web
   user   need modules: Cloud Loadbalancer and Spring Reactive Web
   ```

2. Implement

> Note:
>
> refactor package name

refactor application.properties

```
spring.application.name=user
server.port=8888  // app will run on the port
```

3. Run App

```
mvn spring-boot:run
```

run on multiple port

```
mvn spring-boot:run -Dspring-boot.run.arguments=--server.port=9999
```

test in browser (8888 is balance server)

```
localhost:8888/hi
```



```java
@Override
public Flux<List<ServiceInstance>> get() {
    return Flux.just(Arrays
            .asList(new DefaultServiceInstance(serviceId + "1", serviceId, "localhost", 8090, false),
                    new DefaultServiceInstance(serviceId + "2", serviceId, "localhost", 9092, false),
                    new DefaultServiceInstance(serviceId + "3", serviceId, "localhost", 9999, false)));
}
```

balance server will balance to these three ports

once a target port got some problems, you may see browser will get error

but refresh it, it will be ok, because it is balanced to another ok port

