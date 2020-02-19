### 只有确定按钮的弹框  

以 https://www.w3school.com.cn/tiy/t.asp?f=js_alert 里弹框举例。  

Java 代码  
``` java
import org.openqa.selenium.Alert;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class HandleAlert {
    public static void main(String[] args) {

        // 加载游览器驱动
        WebDriver driver = new ChromeDriver();

        // 打开 https://www.w3school.com.cn/tiy/t.asp?f=js_alert
        driver.get("https://www.w3school.com.cn/tiy/t.asp?f=js_alert");

        // 通过 id 定位的方式切换到 iframe
        driver.switchTo().frame("iframeResult");

        // 点击"试一试" button
        driver.findElement(By.tagName("button")).click();

        // 切换到弹出来的 alert
        Alert alert = driver.switchTo().alert();

        // 点击确定
        alert.accept();
    }
}
```  

Python 代码  
``` python
#!/usr/bin/env python3

from selenium import webdriver

# 加载 Chrome 游览器驱动
browser = webdriver.Chrome(executable_path="apps/chromedriver.exe")

# 打开 https://www.w3school.com.cn/tiy/t.asp?f=js_alert
browser.get("https://www.w3school.com.cn/tiy/t.asp?f=js_alert")

# 通过 id 定位的方式切换到 iframe
browser.switch_to.frame("iframeResult")

# 点击"试一试" button
browser.find_element_by_tag_name("button").click()

# 切换到弹出来的 alert, 并点击确定
browser.switch_to.alert().accept()
```