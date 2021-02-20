---
layout: hidden_page
title: SpringMVC学习笔记
---

* auto-gen TOC:
{:toc}
# SpringMVC

官方文档：https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/web.html

辅助资料：https://www.w3cschool.cn/spring_mvc_documentation_linesh_translation

教程：http://c.biancheng.net/spring_mvc/

https://www.cnblogs.com/wormday/p/8435617.html



SpringMVC是基于`Servlet`API的Web框架



## DispatcherServlet

所有的请求都由`DispatcherServlet`管理并分发到各个具体的控制器中。因此，需要在`web.xml`中注册该Servlet，或通过`ServletRegistration.Dynamic`动态注册。



### 支持的Bean类型

| Bean 类型                                 | 备注                                                         |
| :---------------------------------------- | :----------------------------------------------------------- |
| `HandlerMapping`                          | Map a request to a handler along with a list of [interceptors](https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/web.html#mvc-handlermapping-interceptor) for pre- and post-processing. The mapping is based on some criteria, the details of which vary by `HandlerMapping` implementation.The two main `HandlerMapping` implementations are `RequestMappingHandlerMapping` (which supports `@RequestMapping` annotated methods) and `SimpleUrlHandlerMapping` (which maintains explicit registrations of URI path patterns to handlers). |
| `HandlerAdapter`                          | Help the `DispatcherServlet` to invoke a handler mapped to a request, regardless of how the handler is actually invoked. For example, invoking an annotated controller requires resolving annotations. The main purpose of a `HandlerAdapter` is to shield the `DispatcherServlet` from such details. |
| `HandlerExceptionResolver`                | Strategy to resolve exceptions, possibly mapping them to handlers, to HTML error views, or other targets. See [Exceptions](https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/web.html#mvc-exceptionhandlers). |
| `ViewResolver`                            | Resolve logical `String`-based view names returned from a handler to an actual `View` with which to render to the response. See [View Resolution](https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/web.html#mvc-viewresolver) and [View Technologies](https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/web.html#mvc-view). |
| `LocaleResolver`, `LocaleContextResolver` | Resolve the `Locale` a client is using and possibly their time zone, in order to be able to offer internationalized views. See [Locale](https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/web.html#mvc-localeresolver). |
| `ThemeResolver`                           | Resolve themes your web application can use — for example, to offer personalized layouts. See [Themes](https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/web.html#mvc-themeresolver). |
| `MultipartResolver`                       | Abstraction for parsing a multi-part request (for example, browser form file upload) with the help of some multipart parsing library. See [Multipart Resolver](https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/web.html#mvc-multipart). |
| `FlashMapManager`                         | Store and retrieve the “input” and the “output” `FlashMap` that can be used to pass attributes from one request to another, usually across a redirect. See [Flash Attributes](https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/web.html#mvc-flash-attributes). |

如果`WebApplicationContext`中未声明对应类型的`bean`，那么将会使用 [`DispatcherServlet.properties`](https://github.com/spring-projects/spring-framework/blob/master/spring-webmvc/src/main/resources/org/springframework/web/servlet/DispatcherServlet.properties)中的默认实现。



### 请求处理流程 (文档1.1.5) *







## Controller允许的返回值

https://www.cnblogs.com/guo-rong/p/9199511.html

https://blog.csdn.net/u011001084/article/details/52846791



## 零散笔记

-   Spring围绕`DispatcherServlet`设计
-   `ContextLoaderListener `会负责实例化`ApplicationContext`容器



## 问题

-   SpringMVC启动流程？



# 跟着教程走

## 创建简单Controller

创建一个`bean`，继承`Controller`接口，其`id`设置为路径

```java
import org.springframework.stereotype.Component;
import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.Controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@Component("/plain")
public class PlainController implements Controller {

    @Override
    public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
        return new ModelAndView("plain");
    }
}
```



## 内部视图解析器

```xml
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/jsp/"/>
    <property name="suffix" value=".jsp"/>
</bean>
```



## 请求处理方法

对于`@RequestMapping`注释的方法，若要使用`Servlet API`类型，可以将其作为方法的参数类型。

```java
@GetMapping("/hello")
public String hello(HttpSession session, HttpServletRequest request){
    return "hello";
}
```

可以从`HttpServletRequest`中得到参数

还可以添加`org.springframework.ui.Model`类型

```java
@GetMapping("/hello")
public String hello(Model model){
    /*在视图中可以使用EL表达式${success}取出model中的值*/
    model.addAttribute("a", "b");
    return "hello";
}
```

可以使用参数来接受post/get的数据，相当于使用`@RequestParam(required = false) `注解

```java
@RequestMapping("/login")
public String hello(String attr){
    logger.warn(attr);
    return "login";
}
```

访问`http://localhost:8080/hello?=123`输出日志"123"，访问`http://localhost:8080/hello`则`attr`为`null`

甚至可以使用POJO接收参数

```java
public class User {
    private String username;
    private String password;

	// getter/setter/toString省略
}
```

```java
@RequestMapping("/login")
public String hello(User attr, String username){
    logger.warn(attr);
    logger.warn(username);
    return "login";
}
```

当访问`login?username=123&password=456`时，`attr.username`与`username`的值都为"123"

还可以使用`@PathVariable `/`@ModelAttribute`注解



## Service 与 Controller 的区别 *



## @ModelAttribute

被 @ModelAttribute 注解的方法将在每次调用该控制器类的请求处理方法前被调用。

```java
@ModelAttribute("timestamp")
public Long isPermitted(Model model){
    return System.currentTimeMillis();
}

@RequestMapping("/login")
public String hello(Model model, String timestamp){
    logger.warn(timestamp);
    logger.warn(model.getAttribute("timestamp"));
    return "login";
}
```

访问`http://localhost:8080/login?timestamp=12580`时，得到日志

```
top.chgtaxihe.springmvc.HelloController.hello 12580
top.chgtaxihe.springmvc.HelloController.hello 1612859868434
```

