# Spring Boot中使用thymeleaf  

> Thymeleaf是前端模板引擎。因为Spring Boot使用的是内嵌版本的tomcat，不支持使用jsp

## 引入thymeleaf  

在pom.xml中加入thymeleaf的依赖  

```xml
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
```

在 html文件中加入使用thymeleaf的声明  

``` xml
<html lang="en" xmlns:th="http://www.thymeleaf.org">
```

举例如下：  

``` xml
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8"/>
    <title>Hello Thymeleaf!</title>
</head>
<body>
    <p th:text="'Hello, ' + ${name} + '!'" />
</body>
</html>
```

## 语法规则  

使用形式：**th:[html属性]=[表达式]**  

含义：用表达式的值代替html属性的值

### html属性

所有的html属性都能使用th进行替换。`th:id`代表替换id，`th:text`代表替换文本  

### 表达式  

支持的表达式可分为以下几类：

* 变量表达式：`${...}`  
* 星号表达式：`*{...}`  
* 井号表达式：`#{...}`  
* URL表达式：`@{...}`  
* 片段表达式：`~{...}`    

#### 变量表达式

顾名思义，获取变量值。如`<p th:text="'Hello, ' + ${name} + '!'" />`，`${name}`会从ModelAndView对象中获取name属性的值  

#### 星号表达式  

星号表达式与变量表达式的功能相同，`th:text=${hello}`等同于`th:text=*{hello}`。但星号表达式与`th:object`配合使用时，会把`th:object`认定为选定对象。举例说明：  

``` html
<div th:object="${session.user}">
  <p>Name: <span th:text="*{firstName}">Sebastian</span>.</p>
  <p>Surname: <span th:text="*{lastName}">Pepper</span>.</p>
  <p>Nationality: <span th:text="*{nationality}">Saturn</span>.</p>
</div>
```

上面的html等同于下面的html：  

``` html
<div th:object="${session.user}">
  <p>Name: <span th:text="${session.user.firstName}">Sebastian</span>.</p>
  <p>Surname: <span th:text="${session.user.lastName}">Pepper</span>.</p>
  <p>Nationality: <span th:text="${session.user.nationality}">Saturn</span>.</p>
</div>
```

#### 井号表达式  

井号表达式适用于国际化取值，允许从一个外部文件获取区域的文字信息。  

#### URL表达式  

URL表达式就是重写URL。  

比如想要访问`http://localhost:8080/gtvg/order/details?orderId=3`，可写成如下形式：  

``` html
<a href="details.html" th:href="@{http://localhost:8080/gtvg/order/details(orderId=${o.id})}">view</a>
```

比如想要访问`/gtvg/order/details?orderId=3`，可写成如下形式：  

``` html
<a href="details.html" th:href="@{/order/details(orderId=${o.id})}">view</a>
```

比如想要访问`/gtvg/order/3/details`，可写成如下形式：  

``` html
<a href="details.html" th:href="@{/order/{orderId}/details(orderId=${o.id})}">view</a>
```

#### 片段表达式  

待补充