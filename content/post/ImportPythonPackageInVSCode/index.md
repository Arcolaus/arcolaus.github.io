+++
title = '在VSCode中Python导入父级目录下的package，而避免使用sys.path()方法'
date = 2024-09-28T20:19:31+08:00
draft = false
categories = [
    "Python"
]
tags = [
	"Python",
	"VS Code"
]
+++

最近在写的一个Python项目如下(只用关心`src`目录和`test`目录)：
```bash
smartQA
├── readme.md
├── requirements.txt
├── src
│   ├── __init__.py
│   ├── api
│   │   ├── __init__.py
│   │   └── app.py
│   ├── backend
│   │   ├── __init__.py
│   │   └── models_config.py
│   └── utils
│       ├── __init__.py
│       ├── db.py
│       ├── model_load.py
│       └── promot.py
└── tests
    ├── __init__.py
    ├── test.py
    ├── test_notebook
    │   ├── __init__.py
    │   └── test_api.ipynb
    └── visualized_response.json
```
我想在`tests/test.py`文件中`from src.utils.db`，但是会提示`No module named 'src'`，也就是解释器并没有找到这个package，在执行`test.py`文件的时候环境变量中并没有将其他目录包含进来。网上有两种方式：
1. 使用`sys.path()`方法
2. 在项目目录下创建`.vscode/launch.json`文件
个人觉得第一中方法并不规范，而第二种方式增加里冗余文件，所以尝试找到一种别的更加优雅的方式，如下

在VSCode搜索设置：`python.analysis.extraPaths`，增加项设置为`${workspaceFolder}`