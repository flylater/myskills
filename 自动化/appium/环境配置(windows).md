## Python环境配置  

### 安装nodejs  
安装最新版的nodejs，官网：https://nodejs.org/en/  

### 安装appium  
nodejs安装完成之后，可以使用npm安装appium.  
由于国外源被墙，需要指定国内源才能安装成功.  
步骤如下：  
用管理员模式打开cmd
1. 设置国内源  
在cmd里输入：`npm config set registry https://registry.npm.taobao.org`  (指定为淘宝源)
2. 安装appium  
在cmd里输入：：`npm install -g appium`  

安装完成后，可以在cmd里输入`appium -v`来查看appium的版本。如果安装成功，在cmd里输入`appium`就可以启动appium。  

注：如果已经安装过旧版本的appium，或者之前的appium卸载不完全，可以按以下步骤重新安装appium：
1. 卸载appium：`npm uninstall -g appium`  
2. 清理缓存：`npm cache verify`或`npm cache clean --force`  
3. 重新安装appium：`npm install -g appium`  

### 安装

