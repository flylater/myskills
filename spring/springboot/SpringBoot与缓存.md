# SpringBoot与缓存  

## 缓存注解  

### @EnableCaching  

开启基于注解的缓存，此注解需要加在SpringBoot的启动类上  。

例如：  

``` java
import org.mybatis.spring.annotation.MapperScan;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cache.annotation.EnableCaching;

@SpringBootApplication
@EnableCaching
@MapperScan("com.rszhang.mybatisdemo.dao")
public class MybatisdemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(MybatisdemoApplication.class, args);
    }

}
```



### @Cacheable  

根据方法的请求参数对其结果进行缓存，以后再请求相同的数据，直接从缓存中获取，不用调用方法。

#### @Cacheable的属性

@Cachable有以下几个属性：

* cacheNames/value： 缓存的名字，在spring配置文件中定义，必须指定至少一个，是数组的方式。
* key：缓存数据使用的key。可以为空，如果为空，则按照方法的所有参数值进行组合；如果不为空，则要按照SpEL表达式进行编写。
* keyGenerator：缓存数据时key生成策略。可以自己指定key的生成策略。key和keyGenerator只能二选一。
* cacheManager：缓存管理器。与cacheResolver二选一。
* condition：指定符合条件的情况下才缓存。使用SpEL表达式编写，可以为空。在调用方法之前之后都能判断
* unless：否决缓存。当unless指定的条件为true的时候，方法的返回值就不会被缓存。只在方法执行之后判断。
* sync：是否使用异步模式。为true的情况下，不支持unless。



#### SpEL可用的元数据 

| 名字          | 位置               | 描述                                                         | 示例                 |
| ------------- | ------------------ | ------------------------------------------------------------ | -------------------- |
| methodName    | root object        | 当前被调用的方法名                                           | #root.methodName     |
| method        | root object        | 当前被调用的方法                                             | #root.method.name    |
| target        | root object        | 当前被调用的目标对象                                         | #root.target         |
| targetClass   | root object        | 当前被调用的目标对象类                                       | #root.targetClass    |
| args          | root object        | 当前被调用的方法的参数列表                                   | #root.args[0]        |
| caches        | root object        | 当前方法调用使用的缓存列表(如@ Cacheable(value={"cache1","cache2"}) ), 则有两个 cache | #root.caches[0].name |
| argument name | evaluation context | 方法参数的名字 . 可以直接 #参数名 ,也可以使用 #p0或#a0 的形式,0代表参数的索引; | #iban 、 #a0 、 #p0  |
| result        | evaluation context | 方法执行后的返回值(仅当方法执行之后的判断有效,如‘ unless’ , ’cache put’ 的表达式 ’cache evict’ 的表达式beforeInvocation=false ) | #result              |

> #root在使用时可以省略不写。#root.args[0]可以写成args[0]

#### @Cacheable的运行流程  

1. 方法运行之前，先去查询Cache，按照cacheNames/value指定的名字去获取，第一次获取缓存如果没有Cache组件会自动创建。

2. 去Cache中查找缓存的内容，查找的方式是通过key去查找。key是按照某种策略生成的，默认使用keyGenerator接口生成，默认的实现类是SimpleKeyGenerator。

   SimpleKeyGenerator类生成key的策略为：

   * 如果没有参数，key=new SimpleKey();
   * 如果有一个参数，key=参数的值
   * 如果有多个参数，key=new SimpleKey(params)

3. 没有查到缓存就调用目标方法。

4. 将目标方法返回的结果，放进缓存中。



#### 定制keyGenerator  

编写配置类

``` java
package com.rszhang.mybatisdemo.config;

import org.springframework.cache.interceptor.KeyGenerator;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import java.lang.reflect.Method;
import java.util.Arrays;

@Configuration
public class MyCacheConfig {

    @Bean("myKeyGenerator")
    public KeyGenerator keyGenerator() {
        return new KeyGenerator() {

            @Override
            public Object generate(Object o, Method method, Object... objects) {
                return method.getName()+"[" + Arrays.asList(objects).toString() + "]";
            }
        };
    }

}
```

使用时指定定制的策略  

```java
@Cacheable(value = "query", key = "myKeyGenerator")
```



### @CachePut  

即调用方法，又更新缓存。

运行流程：

1.  先调用目标方法
2. 将目标方法的结果缓存起来



### @CacheEvict  

清除缓存。

属性：

* allEntries：是否清空所有缓存内容,缺省为 false,如果指定为true,则方法调用后将立即清空所有缓存
* beforeInvocation：是否在方法执行前就清空,缺省为 false,如果指定为 true,则在方法还没有执行的时候就清空缓存,缺省情况下,如果方法执行抛出异常,则不会清空缓存

