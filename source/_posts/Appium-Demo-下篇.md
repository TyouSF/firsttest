---
title: Appium Demo 下篇
date: 2017-04-07 16:11:25
categories:
- Appium
tags:
- python
- appium
- 测试
keywords:
---

{% asset_img appium1.png %}

{% cq %}
一个Appium的Demo之旅

TyouSF
{% endcq %}

<!--more-->

本文我们将使用Python语言编写第一个基于Appium的自动化测试脚本。

脚本实际运行效果：
在Android模拟器中，自行调用计算器，完成一个简单的数学计算：1+1

编写前必须要声明的注意事项：

- Appium当前版本为：1.4.16.1  
由于版本原因，当前该版本最高支持到Android M，及Android 6.0，对应Android API 23
- 安卓模拟器的创建  
基于上一条Appium的原因，对7.0以上的Android版本支持不太友好，存在Bug，如果您坚持使用基于7.0以上创建的安卓模拟器，运行过程中可能会遇到各种问题，不建议采用。建议创建一个基于Android 6.0 版本的模拟器，如果您还不知道怎么创建，可详细查阅{% post_link "Appium-Demo-上篇" %}

# 启动Appium

运行Appium客户端，并启动Appium服务。启动图如下：
{% asset_img appium2.png %}
{% asset_img appium3.png %}

# 启动Android AVD

打开Android Studio启动创建好的安卓模拟器即可
{% asset_img avd1.png %}

# 编写Python脚本

```python
from appium import webdriver

desired_caps = {}
desired_caps['platformName'] = 'Android'
desired_caps['platformVersion'] = '4.4.2'
desired_caps['deviceName'] = 'Android Emulator'
desired_caps['appPackage'] = 'com.android.calculator2'
desired_caps['appActivity'] = '.Calculator'

driver = webdriver.Remote('http://localhost:4723/wd/hub', desired_caps)

driver.find_element_by_name("1").click()

driver.find_element_by_name("+").click()

driver.find_element_by_name("1").click()

driver.find_element_by_name("=").click()

driver.quit()
```

# 执行脚本

假设您编写的脚本名称为：`demo.py`
```
python demo.py
```

如果没有异常，运行脚本后，您便可以在Android AVD中看到整个执行过程。就像这样：↓
{% asset_img 70914.gif %}