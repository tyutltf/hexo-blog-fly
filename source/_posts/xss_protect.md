---
title: XSS和CSRF保护
author: 雨轩恋
top: false
cover: false
toc: true
mathjax: false
date: 2019-11-09 11:01:15
img:
coverImg:
password:
summary:
    Flask网站如何有效的避免XSS和CSRF攻击
tags:
  - 网站防护
categories:
  - Flask
---



### XSS
> xss攻击即跨站脚本攻击，攻击者将通过恶意代码注入到被攻击者的网站中，用户一旦访问就会执行被注入的恶意脚本。例如在用户评论界面输入代码


```
<script>alert('hhhh')</script>
```

就会弹出 hhhh 字样。

#### 如何防护xss

- HTML转义

可以使用jinja2的escape函数对用户输入的数据进行转义。

- 验证用户输入

对用户输入的数据进行过滤

### CSRF攻击

如果用户访问了A网站后不退出，继续访问了危险的B网站，那么B网站就有可能获取A网站的cookie而伪装成A网站的用户来进行操作。

#### 主要防范措施

- 正确使用HTTP方法，提交数据时候使用POST。
- 使用CSRF令牌校验

Flask有一个模块叫 flask_csrfprotect 这个模块可以用来防护CSRF攻击


```
from flask_wtf.csrf import CSRFProtect
app.config['SECRET_KEY'] = os.urandom(24)
CSRFProtect(app)
```


在前端页面的form表单加入这一行代码即可
```
<input type="hidden" name="csrf_token" value="{{ csrf_token() }}" />
```



