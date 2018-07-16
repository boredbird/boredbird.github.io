---
title: Jupyter notebook默认启动路径配置
date: 2018-07-16 14:53:12
categories: "Python"
tags:
     - Python
description: Jupyter notebook默认启动路径配置
---

配置 Jupyter notebook
`jupyter notebook --generate-config`

    D:\Program Files (x86)\PowerCmd>jupyter notebook --generate-config
    Writing default config to: C:\Users\zhangchunhui\.jupyter\jupyter_notebook_config.py

修改jupyter_notebook_config.py
    ## The directory to use for notebooks and kernels.
    c.NotebookApp.notebook_dir = 'E:\Code'


<!--more-->
