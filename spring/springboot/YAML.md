# YAML  

## 基本语法  

格式为：`K:(空格)V`，以**空格**的缩进来控制层级关系  

* 大小写敏感  
* 使用缩进表示层级关系  
* 缩进不允许使用tab，只允许空格  
* 缩进的空格数无要求，左对齐的一列数据，都属于同一个层级  
* '#'表示注释  
* ""：双引号，不会转义字符串里面的特殊字符  
* ''：单引号，会转义特殊字符  



## 记录方式  

### 普通值(数字，字符串，布尔值)  

`K:(空格)V`, 字符串默认不用加上单引号或双引号  

### JavaBean对象、Map  

``` yaml
K:
 K1: V1
 K2: V2
```

也可以行内表示：  

```yaml
K: {K1: V1,K2: V2}
```

### 数组、集合  

```yaml
K:
 - V1
 - V2
```

也可以行内表示：  

```yaml
K: [V1,V2]
```



## YAML文件的值注入  

可以使用@ConfigurationProperties将配置文件中的每一个属性的值，映射到组件当中。必须是容器中的组件(类上需要加上@Component等证明是容器组件的注解)，才能使用容器提供的@ConfigurationProperties功能。@ConfigurationProperties默认从全局配置文件中取值。  

* 需要加入的依赖  

  ```xml
  <!-- 导入配置文件处理器 -->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-configuration-processor</artifactId>
              <optional>true</optional>
          </dependency>
  ```

举例说明，编写一个yml文件内容如下：  

```yaml
server:
  port: 8081

person:
  name: Tom
  age: 20
  birth: 2000/01/01
  address:
    province: shanxi
    city: xian
```

然后编写一个bean类Address、Person  

```java
public class Address {

    private String province;
    private String city;

    public String getProvince() {
        return province;
    }

    public void setProvince(String province) {
        this.province = province;
    }

    public String getCity() {
        return city;
    }

    public void setCity(String city) {
        this.city = city;
    }

    @Override
    public String toString() {
        return "Address{" +
                "province='" + province + '\'' +
                ", city='" + city + '\'' +
                '}';
    }
}
```

```java
import java.util.Date;

@Component
@ConfigurationProperties(prefix = "person")
public class Person {

    private String name;
    private Integer age;
    private Date birth;
    private Address address;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public Date getBirth() {
        return birth;
    }

    public void setBirth(Date birth) {
        this.birth = birth;
    }

    public Address getAddress() {
        return address;
    }

    public void setAddress(Address address) {
        this.address = address;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", birth=" + birth +
                ", address=" + address +
                '}';
    }
}
```

运行Spring Boot应用，Person类就会获取yml里面对应的值



## 通过profile配置多环境  

YAML通过`---`来分割配置文件的内容，可通过profiles指定激活哪一部分内容  

``` yaml
spring:
  profiles:
    active: prod

---
server:
  port: 8082
spring:
  profiles: dev

---
server:
  port: 8083
spring:
  profiles: prod
```

如上面的YAML文件，指定prod部分的配置为激活配置，当Spring Boot启动时，端口号为8083





