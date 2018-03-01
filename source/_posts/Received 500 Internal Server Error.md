---
title: Received "500: Internal Server Error"
date: 2018-03-01 16:53:12
categories: "Python"
tags:
     - Python
description: Received "500: Internal Server Error"
---
## 问题
使用twine在whl文件打包上传到pypi时，出现如下错误：

![](assets/python/20180301162329.png)

换种方式上传：
```
    PS E:\Code\woe> python setup.py sdist upload
    running sdist
    running egg_info
    writing requirements to woe.egg-info\requires.txt
    writing woe.egg-info\PKG-INFO
    writing top-level names to woe.egg-info\top_level.txt
    writing dependency_links to woe.egg-info\dependency_links.txt
    reading manifest file 'woe.egg-info\SOURCES.txt'
    reading manifest template 'MANIFEST.in'
    writing manifest file 'woe.egg-info\SOURCES.txt'
    running check
    creating woe-0.1.4
    creating woe-0.1.4\examples
    creating woe-0.1.4\woe
    creating woe-0.1.4\woe.egg-info
    copying files to woe-0.1.4...
    copying LICENSE.txt -> woe-0.1.4
    copying MANIFEST.in -> woe-0.1.4
    copying README.rst -> woe-0.1.4
    copying setup.py -> woe-0.1.4
    copying examples\HereWeGo.py -> woe-0.1.4\examples
    copying examples\README.rst -> woe-0.1.4\examples
    copying examples\UCI_Credit_Card.csv -> woe-0.1.4\examples
    copying examples\config.csv -> woe-0.1.4\examples
    copying woe\GridSearch.py -> woe-0.1.4\woe
    copying woe\__init__.py -> woe-0.1.4\woe
    copying woe\config.py -> woe-0.1.4\woe
    copying woe\eval.py -> woe-0.1.4\woe
    copying woe\feature_process.py -> woe-0.1.4\woe
    copying woe\ftrl.py -> woe-0.1.4\woe
    copying woe.egg-info\PKG-INFO -> woe-0.1.4\woe.egg-info
    copying woe.egg-info\SOURCES.txt -> woe-0.1.4\woe.egg-info
    copying woe.egg-info\dependency_links.txt -> woe-0.1.4\woe.egg-info
    copying woe.egg-info\requires.txt -> woe-0.1.4\woe.egg-info
    copying woe.egg-info\top_level.txt -> woe-0.1.4\woe.egg-info
    Writing woe-0.1.4\setup.cfg
    Creating tar archive
    removing 'woe-0.1.4' (and everything under it)
    running upload
    Password:
    Submitting dist\woe-0.1.4.tar.gz to https://upload.pypi.org/legacy/
    Upload failed (403): Invalid or non-existent authentication information.
    error: Upload failed (403): Invalid or non-existent authentication information.
    PS E:\Code\woe>
    PS E:\Code\woe> python setup.py sdist upload
    running sdist
    running egg_info
    writing requirements to woe.egg-info\requires.txt
    writing woe.egg-info\PKG-INFO
    writing top-level names to woe.egg-info\top_level.txt
    writing dependency_links to woe.egg-info\dependency_links.txt
    reading manifest file 'woe.egg-info\SOURCES.txt'
    reading manifest template 'MANIFEST.in'
    writing manifest file 'woe.egg-info\SOURCES.txt'
    running check
    creating woe-0.1.4
    creating woe-0.1.4\examples
    creating woe-0.1.4\woe
    creating woe-0.1.4\woe.egg-info
    copying files to woe-0.1.4...
    copying LICENSE.txt -> woe-0.1.4
    copying MANIFEST.in -> woe-0.1.4
    copying README.rst -> woe-0.1.4
    copying setup.py -> woe-0.1.4
    copying examples\HereWeGo.py -> woe-0.1.4\examples
    copying examples\README.rst -> woe-0.1.4\examples
    copying examples\UCI_Credit_Card.csv -> woe-0.1.4\examples
    copying examples\config.csv -> woe-0.1.4\examples
    copying woe\GridSearch.py -> woe-0.1.4\woe
    copying woe\__init__.py -> woe-0.1.4\woe
    copying woe\config.py -> woe-0.1.4\woe
    copying woe\eval.py -> woe-0.1.4\woe
    copying woe\feature_process.py -> woe-0.1.4\woe
    copying woe\ftrl.py -> woe-0.1.4\woe
    copying woe.egg-info\PKG-INFO -> woe-0.1.4\woe.egg-info
    copying woe.egg-info\SOURCES.txt -> woe-0.1.4\woe.egg-info
    copying woe.egg-info\dependency_links.txt -> woe-0.1.4\woe.egg-info
    copying woe.egg-info\requires.txt -> woe-0.1.4\woe.egg-info
    copying woe.egg-info\top_level.txt -> woe-0.1.4\woe.egg-info
    Writing woe-0.1.4\setup.cfg
    Creating tar archive
    removing 'woe-0.1.4' (and everything under it)
    running upload
    Submitting dist\woe-0.1.4.tar.gz to https://upload.pypi.org/legacy/
    Server response (200): OK
    PS E:\Code\woe> twine upload dist/*
    Uploading distributions to https://upload.pypi.org/legacy/
    Uploading woe-0.1.4-py2-none-any.whl
    Received "500: Internal Server Error" Package upload appears to have failed.  Retry 1 of 5
    Uploading woe-0.1.4-py2-none-any.whl
    Received "500: Internal Server Error" Package upload appears to have failed.  Retry 2 of 5
    Uploading woe-0.1.4-py2-none-any.whl
    Received "500: Internal Server Error" Package upload appears to have failed.  Retry 3 of 5
    Uploading woe-0.1.4-py2-none-any.whl
    Received "500: Internal Server Error" Package upload appears to have failed.  Retry 4 of 5
    Uploading woe-0.1.4-py2-none-any.whl
    Received "500: Internal Server Error" Package upload appears to have failed.  Retry 5 of 5
    HTTPError: 500 Server Error: Internal Server Error for url: https://upload.pypi.org/legacy/
    PS E:\Code\woe> python setup.py bdist_wheel upload
    running bdist_wheel
    running build
    running build_py
    installing to build\bdist.win-amd64\wheel
    running install
    running install_lib
    creating build\bdist.win-amd64\wheel
    creating build\bdist.win-amd64\wheel\woe
    copying build\lib\woe\config.py -> build\bdist.win-amd64\wheel\.\woe
    copying build\lib\woe\eval.py -> build\bdist.win-amd64\wheel\.\woe
    copying build\lib\woe\feature_process.py -> build\bdist.win-amd64\wheel\.\woe
    copying build\lib\woe\ftrl.py -> build\bdist.win-amd64\wheel\.\woe
    copying build\lib\woe\GridSearch.py -> build\bdist.win-amd64\wheel\.\woe
    copying build\lib\woe\__init__.py -> build\bdist.win-amd64\wheel\.\woe
    running install_egg_info
    running egg_info
    writing requirements to woe.egg-info\requires.txt
    writing woe.egg-info\PKG-INFO
    writing top-level names to woe.egg-info\top_level.txt
    writing dependency_links to woe.egg-info\dependency_links.txt
    reading manifest file 'woe.egg-info\SOURCES.txt'
    reading manifest template 'MANIFEST.in'
    writing manifest file 'woe.egg-info\SOURCES.txt'
    Copying woe.egg-info to build\bdist.win-amd64\wheel\.\woe-0.1.4-py2.7.egg-info
    running install_scripts
    creating build\bdist.win-amd64\wheel\woe-0.1.4.dist-info\WHEEL
    running upload
    Submitting E:\Code\woe\dist\woe-0.1.4-py2-none-any.whl to https://upload.pypi.org/legacy/
    Server response (200): OK
    PS E:\Code\woe> twine upload dist/*
    Uploading distributions to https://upload.pypi.org/legacy/
    Uploading woe-0.1.4-py2-none-any.whl
    Uploading woe-0.1.4-py3-none-any.whl
    Uploading woe-0.1.4-py2-none-any.tar.gz
```

如上，最后原来是没有.pypirc文件，在自己用户根路径下新建，内容如下：
```
[distutils]
index-servers = pypi

[pypi]
repository: https://upload.pypi.org/legacy/
username: boredbird
password: <密码>
```
最后，如上才上传成功（一开始用python setup.py 上传成功了一个文件，等了一会twine也可以用了，就能够批量上传到pypi了）。
