xml配置  
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- 组件扫描 -->
    <context:component-scan base-package="com.atguigu.spring.aspectJ.annotation"></context:component-scan>

    <!-- 基于注解使用AspectJ: 主要的作用是为切面中通知能作用到的目标类生成代理-->
    <aop:aspectj-autoproxy/>
</beans>
```  

切面类  
``` java
package com.atguigu.spring.aspectJ.annotation;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.springframework.core.annotation.Order;
import org.springframework.stereotype.Component;

import java.util.Arrays;

/**
 * 日志切面
 * @author : Flylater
 * @version : 1.0
 * @date : 2020/4/3
 */
@Component  // 标识为一个组件
@Aspect     // 标识为一个切面
@Order(1)      // 设置切面的优先级, 值越小优先级越高
public class LoggingAspect {

    /**
     * 声明切入点表达式
     */
    @Pointcut("execution(* com.atguigu.spring.aspectJ.annotation.*.*(..))")
    public void declarePoint() {

    }

    /**
     * 前置通知：在目标方法执行之前执行
     */
    @Before("execution(public int com.atguigu.spring.aspectJ.annotation.ArithmeticCalculatorImpl.add(int, int))")
    public void beforMethod(JoinPoint joinPoint) {
        // 获取方法的参数
        Object[] args = joinPoint.getArgs();
        // 获取方法的名字
        String methodName = joinPoint.getSignature().getName();
        System.out.println("LoggingAspect===> The method " + methodName + " begin with " + Arrays.asList(args));
    }

    /**
     * 后置通知：在目标方法之后执行.不管目标方法有没有抛出异常,不能获取方法的结果
     * 连接点对象：JoinPoint
     */
//    @After("execution(* com.atguigu.spring.aspectJ.annotation.*.*(..))")
    @After("declarePoint()")
    public void afterMethod(JoinPoint joinPoint) {
        // 方法的名字
        String methodName = joinPoint.getSignature().getName();

        System.out.println("LoggingAspect==> the method " + methodName + " ends.");

    }

    /**
     * 返回通知：在目标方法正常执行结束后执行，可以获取到方法的返回值
     */
    @AfterReturning(value = "execution(* com.atguigu.spring.aspectJ.annotation.*.*(..))", returning="result")
    public void afterReturningMethod(JoinPoint joinPoint, Object result) {
        // 方法的名字
        String methodName = joinPoint.getSignature().getName();
        System.out.println("LoggingAspect==> The method " + methodName + " end with :" + result);

    }

    /**
     * 异常通知：在目标方法抛出异常后执行
     */
    @AfterThrowing(value = "execution(* com.atguigu.spring.aspectJ.annotation.*.*(..))", throwing = "ex")
    public void afterThrowingMethod(JoinPoint joinPoint, NullPointerException ex) {
        // 方法的名字
        String methodName = joinPoint.getSignature().getName();

        System.out.println("LoggingAspect==> The method " + methodName + " occurs Exception: " + ex);
    }

    /**
     * 环绕通知：环绕着目标方法执行。可以理解是前置、后置、返回、异常 通知的结合体，更像是动态代理的整个过程
     */
    @Around("execution(* com.atguigu.spring.aspectJ.annotation.*.*(..))")
    public Object aroundiMethod(ProceedingJoinPoint pjp) {

        // 执行目标方法
        try {
            // 前置通知
            Object result = pjp.proceed();
            // 返回通知
            return result;
        } catch (Throwable throwable) {
            // 异常通知
            throwable.printStackTrace();
        } finally {
            // 后置通知
        }
        return null;
    }

}
```