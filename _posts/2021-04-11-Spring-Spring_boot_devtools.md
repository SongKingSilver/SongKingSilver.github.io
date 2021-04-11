---
layout: post
title: "Spring boot devtools"
categories:
  - Spring
tags:
  - 스프링
  - 스프링 개발 라이브러리
---

spring boot devtools은 스프링 개발시 편의성을 주는 라이브러리이다.
대표적으로 실시간으로 변경이 있을때마다 어플을 재시작시켜 보여주는기능이 있다.

```java
//build.gradle
dependencies {
	runtimeOnly('org.springframework.boot:spring-boot-devtools')
}
```

intellij registry 설정
ctrl shitf a > registry... > compiler.automake.allow.when.app.running 체크

intellij Compiler 설정
Setting -> Build, Execution, Deployment -> Compiler
Build project automatically 체크