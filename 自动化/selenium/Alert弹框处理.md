## 只有确定按钮的弹框  

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
browser = webdriver.Chrome()

# 打开 https://www.w3school.com.cn/tiy/t.asp?f=js_alert
browser.get("https://www.w3school.com.cn/tiy/t.asp?f=js_alert")

# 通过 id 定位的方式切换到 iframe
browser.switch_to.frame("iframeResult")

# 点击"试一试" button
browser.find_element_by_tag_name("button").click()

# 切换到弹出来的 alert, 并点击确定
browser.switch_to.alert.accept()
```  

## 有确定和取消的弹框  

以 https://www.w3school.com.cn/tiy/t.asp?f=js_confirm 里弹框举例。  

Java代码  
``` java
import org.openqa.selenium.Alert;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class HandleAlert {
    public static void main(String[] args) throws InterruptedException {

        // 加载游览器驱动
        WebDriver driver = new ChromeDriver();

        // 打开 https://www.w3school.com.cn/tiy/t.asp?f=js_confirm
        driver.get("https://www.w3school.com.cn/tiy/t.asp?f=js_confirm");

        // 通过 id 定位的方式切换到 iframe
        driver.switchTo().frame("iframeResult");

        // 点击 Alert 弹框的确定
        driver.findElement(By.tagName("button")).click();
        Alert alert = driver.switchTo().alert();
        alert.accept();

        Thread.sleep(1000);

        // 点击 Alert 弹框的取消
        driver.findElement(By.tagName("button")).click();
        alert.dismiss();
    }
}
```  

Python 代码  
``` python
#!/usr/bin/env python3
import time
from selenium import webdriver

# 加载 Chrome 游览器驱动
browser = webdriver.Chrome()

# 打开 https://www.w3school.com.cn/tiy/t.asp?f=js_confirm
browser.get("https://www.w3school.com.cn/tiy/t.asp?f=js_confirm")

# 通过 id 定位的方式切换到 iframe
browser.switch_to.frame("iframeResult")

# 点击 Alert 弹框的确定
browser.find_element_by_tag_name("button").click()
browser.switch_to.alert.accept()

time.sleep(1)

# 点击 Alert 弹框的取消
browser.find_element_by_tag_name("button").click()
browser.switch_to.alert.dismiss()
```  

## 有输入框的弹框  

以 https://www.w3school.com.cn/tiy/t.asp?f=js_prompt 里弹框举例。  

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

        // 打开 https://www.w3school.com.cn/tiy/t.asp?f=js_prompt
        driver.get("https://www.w3school.com.cn/tiy/t.asp?f=js_prompt");

        // 通过 id 定位的方式切换到 iframe
        driver.switchTo().frame("iframeResult");

        // Alert 弹框里输入 flylater 并点击确定
        driver.findElement(By.tagName("button")).click();
        Alert alert = driver.switchTo().alert();
        alert.sendKeys("flylater");
        alert.accept();
    }
}
```  

Python 代码  
``` python
#!/usr/bin/env python3
from selenium import webdriver

# 加载 Chrome 游览器驱动
browser = webdriver.Chrome()

# 打开 https://www.w3school.com.cn/tiy/t.asp?f=js_prompt
browser.get("https://www.w3school.com.cn/tiy/t.asp?f=js_prompt")

# 通过 id 定位的方式切换到 iframe
browser.switch_to.frame("iframeResult")

# Alert 弹框里输入 flylater 并点击确定
browser.find_element_by_tag_name("button").click()
browser.switch_to.alert.send_keys("flylater")
browser.switch_to.alert.accept()
```  

## 获取弹框里的文本  

以 https://www.w3school.com.cn/tiy/t.asp?f=js_alert_2 里弹框举例。  

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

        // 打开 https://www.w3school.com.cn/tiy/t.asp?f=js_alert_2
        driver.get("https://www.w3school.com.cn/tiy/t.asp?f=js_alert_2");

        // 通过 id 定位的方式切换到 iframe
        driver.switchTo().frame("iframeResult");

        // 获取 Alert 弹框里的文本
        driver.findElement(By.tagName("button")).click();
        Alert alert = driver.switchTo().alert();
        String text = alert.getText();
        alert.accept();
        System.out.println(text);
    }
}
```

Python 代码  
``` python
#!/usr/bin/env python3
from selenium import webdriver

# 加载 Chrome 游览器驱动
browser = webdriver.Chrome()

# 打开 https://www.w3school.com.cn/tiy/t.asp?f=js_alert_2
browser.get("https://www.w3school.com.cn/tiy/t.asp?f=js_alert_2")

# 通过 id 定位的方式切换到 iframe
browser.switch_to.frame("iframeResult")

# 获取 Alert 弹框里的文本
browser.find_element_by_tag_name("button").click()
text = browser.switch_to.alert.text
print(text)
browser.switch_to.alert.accept()
```