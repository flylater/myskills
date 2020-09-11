# SpringBoot与Shiro  

## Shiro的简介  

Apache Shiro是Java的一个安全(权限)框架。  

Shiro可以完成：认证、授权、加密、会话管理、与Web集成、缓存等。



Shiro主要有三大功能模块：

1. Subject：主体，任何可以与应用交互的"用户"。
2. SecurityManager：安全管理器，管理所有Subject，可以配合内部安全组件。(类似于SpringMVC中的DispatcherServlet)。
3. Realms：用于进行权限信息的验证，一般需要自己实现。



Shiro的细分功能：

* Authentication：身份认证/登录(账号密码验证)。
* Authorization：授权，即角色或者权限验证。
* Session Manager：会话管理，用户登录后的session相关管理。
* Cryptography：加密，密码加密等。
* Web Support：Web支持，集成Web环境。
* Caching：缓存，用户信息、角色、权限等缓存到如redis等缓存中。
* Concurrency：多线程并发验证，在一个线程中开启另一个线程，可以把权限自动传播过去。
* Testing：测试支持。
* Run As：允许一个用户假装为另一个用户（如果他们允许）的身份进行访问。
* Remember Me：记住我，登录后，下次再来的话不用登录了。

