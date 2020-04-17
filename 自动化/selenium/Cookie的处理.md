Java 代码  
``` java
import org.openqa.selenium.Cookie;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class HandleCookie {
    public static void main(String[] args) {
        // 加载游览器驱动
        WebDriver driver = new ChromeDriver();
        // 游览器最大化
        driver.manage().window().maximize();

        // 打开网址
        driver.get("http:*******");

        // 构造Cookie对象
        Cookie cookie1 = new Cookie("JSESSIONID", "ZnBa9SLK4wqN6X7OtfCT+t5v");
        Cookie cookie2 = new Cookie("DWRSESSIONID", "Nzu1nhRb4SNf7jC56fXmObGtl3n");

        // 在驱动中加入Cookie信息
        driver.manage().addCookie(cookie1);
        driver.manage().addCookie(cookie2);

        // 打开需要Cookie信息的网址
        driver.get("http:********");
    }
}
```  

Python 代码  
``` python
#!/usr/bin/env python3
import time

from selenium import webdriver
from selenium.webdriver import ActionChains
from selenium.webdriver.common.by import By

# 加载 Chrome 游览器驱动
browser = webdriver.Chrome()

# 游览器最大化
browser.maximize_window()

# 打开 http:******
browser.get("http:******")

# 添加cookie的所有信息
# browser.add_cookie({'domain': '10.221.135.122', 'httpOnly': True, 'name': 'SESSION', 'path': '/cacas/', 'secure': False, 'value': 'e5098998-959e-4f64-82b0-2de7863d55a9'})

# 添加cookie的必要信息
browser.add_cookie({'name': 'SESSION', 'value': 'e5098998-959e-4f64-82b0-2de7863d55a9'})

# 打开需要cookie的网址
browser.get("http://10.221.137.56:8380/capss/abframe/auth/forwardDesktop")
```
