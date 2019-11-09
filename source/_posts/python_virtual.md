---
title: Vscode下Python虚拟环境的安装
author: 雨轩恋
top: false
cover: false
toc: true
mathjax: false
date: 2019-10-09 11:01:15
img:
coverImg:
password:
summary:
    Vscode下python虚拟环境的配置以及使用
tags:
  - Virtual
categories:
  - 软件安装与配置
---




**虚拟环境virtualenvwrapper**
1. 安装

pip install virtualenv 首先得安装 virtualenv 库

pip install virtualenvwrapper-win

配置WORKON_HOME 环境变量

2. 创建虚拟环境

mkvirtualenv textenv

创建虚拟环境并可以直接进入虚拟环境

3. 查看虚拟环境

workon 可以查看虚拟环境

4. 进入虚拟环境

workon textenv 进入虚拟环境

5. 安装依赖包

pip install -r requirements.txt

6. 退出虚拟环境

deactivate

7. 删除虚拟环境

rmvirtualenv textenv

8. 将项目添加到工作目录

python add tab 键

### 以上步骤，在powershell里面 虚拟环境并没有出现，还缺少一步

[看这里可以解决](https://blog.csdn.net/Amio_/article/details/80229179)

> Ctrl + shift + p 打开工作区设置

> 选择在 seetings.json中编辑

> 输入 terminal.integrated.shellArgs.windows

> 配置 如下

```
{
    "python.pythonPath": "D:\\workspace\\python_env\\easyreport\\Scripts\\python.exe",
    "terminal.integrated.shellArgs.windows": [
        "/k",
        "D:\\workspace\\python_env\\easyreport\\Scripts\\activate"
    ]
}
```

> 大功告成

