---
title: pip和pip3的共存问题
date: 2018-03-05 14:53:12
categories: "Python"
tags:
     - Python
description: pip和pip3的共存问题
---
### 问题
在win电脑同时装了python2和python3，为了同时共存，将python3环境下的python.exe改为了python3.exe。
但是导致对应的pip3无法使用。

```
    PS C:\Users\maomaochong> pip3
    Fatal error in launcher: Unable to create process using '"'
```

### 解决方案
>官方的解法是什么？
事实上这个问题几年以前Python社区就给出了官方解决方案，只不过国内一直没有注意到罢了。
我们在安装Python3（>=3.3）时，Python的安装包实际上在系统中安装了一个启动器py.exe，默认放置在文件夹C:\Windows\下面。这个启动器允许我们指定使用Python2还是Python3来运行代码（当然前提是你已经成功安装了Python2和Python3）。


使用pip当Python2和Python3同时存在于windows上时，它们对应的pip都叫pip.exe，所以不能够直接使用 pip install 命令来安装软件包。而是要使用启动器py.exe来指定pip的版本。命令如下：

>py -2 -m pip install XXXX-2

还是表示使用 Python2，-m pip 表示运行 pip 模块，也就是运行pip命令了。

如果是为Python3安装软件，那么命令类似的变成

>py -3 -m pip install XXXX


<!-- more -->

#### #! python2 和 # coding: utf-8 哪个写在前面？
对于Python2用户还有另外一个困惑，Python2要在代码文件顶部增加一行说明，才能够在代码中使用中文。如果指明使用的Python版本也需要在文件顶部增加一行，那哪一行应该放在第一行呢？

`#! python2` 需要放在第一行，编码说明可以放在第二行。所以文件开头应该类似于：

```
#! python2
# coding: utf-8
```

### 例子
```
Windows PowerShell
版权所有 (C) Microsoft Corporation。保留所有权利。

PS C:\Users\maomaochong> pip3
Fatal error in launcher: Unable to create process using '"'
PS C:\Users\maomaochong> pip

Usage:
  pip <command> [options]

Commands:
  install                     Install packages.
  download                    Download packages.
  uninstall                   Uninstall packages.
  freeze                      Output installed packages in requirements format.
  list                        List installed packages.
  show                        Show information about installed packages.
  check                       Verify installed packages have compatible dependencies.
  search                      Search PyPI for packages.
  wheel                       Build wheels from your requirements.
  hash                        Compute hashes of package archives.
  completion                  A helper command used for command completion.
  help                        Show help for commands.

General Options:
  -h, --help                  Show help.
  --isolated                  Run pip in an isolated mode, ignoring
                              environment variables and user configuration.
  -v, --verbose               Give more output. Option is additive, and can be
                              used up to 3 times.
  -V, --version               Show version and exit.
  -q, --quiet                 Give less output. Option is additive, and can be
                              used up to 3 times (corresponding to WARNING,
                              ERROR, and CRITICAL logging levels).
  --log <path>                Path to a verbose appending log.
  --proxy <proxy>             Specify a proxy in the form
                              [user:passwd@]proxy.server:port.
  --retries <retries>         Maximum number of retries each connection should
                              attempt (default 5 times).
  --timeout <sec>             Set the socket timeout (default 15 seconds).
  --exists-action <action>    Default action when a path already exists:
                              (s)witch, (i)gnore, (w)ipe, (b)ackup, (a)bort.
  --trusted-host <hostname>   Mark this host as trusted, even though it does
                              not have valid or any HTTPS.
  --cert <path>               Path to alternate CA bundle.
  --client-cert <path>        Path to SSL client certificate, a single file
                              containing the private key and the certificate
                              in PEM format.
  --cache-dir <dir>           Store the cache data in <dir>.
  --no-cache-dir              Disable the cache.
  --disable-pip-version-check
                              Don't periodically check PyPI to determine
                              whether a new version of pip is available for
                              download. Implied with --no-index.
PS C:\Users\maomaochong> py -3 -m pip install woe
Collecting woe
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/f5/32/ba4d592dfef45338ee04ca90c37b4f3aa345bdeafcad4dcbf654ad0b14c2/woe-0.1.4-py3-none-any.whl
Collecting matplotlib>=2.0.0 (from woe)
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/b6/9c/6ce11b82f9f7276c24711646c3ee43d40f78974ae8e0227a1d2200a44736/matplotlib-2.1.2-cp35-cp35m-win32.whl (8.5MB)
    100% |████████████████████████████████| 8.5MB 81kB/s
Collecting scipy>=0.18.1 (from woe)
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/ab/4d/6468b15538132ffc31112945aa6672a851888b4aad03f0c4710121aff707/scipy-1.0.0-cp35-none-win32.whl (26.0MB)
    100% |████████████████████████████████| 26.0MB 34kB/s
Collecting pandas>=0.19.2 (from woe)
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/be/ae/3eacbdfaf2c47ba4a7eff5ce4e1a7d5f79d87be67d1cb186c238f3118245/pandas-0.22.0-cp35-cp35m-win32.whl (8.2MB)
    100% |████████████████████████████████| 8.2MB 85kB/s
Collecting numpy>=1.11.3 (from woe)
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/8e/12/22cded1311ac12946c4ac51257000427269c115fbf544446548022d154a3/numpy-1.14.1-cp35-none-win32.whl (9.8MB)
    100% |████████████████████████████████| 9.8MB 73kB/s
Collecting six>=1.10 (from matplotlib>=2.0.0->woe)
  Using cached https://pypi.tuna.tsinghua.edu.cn/packages/67/4b/141a581104b1f6397bfa78ac9d43d8ad29a7ca43ea90a2d863fe3056e86a/six-1.11.0-py2.py3-none-any.whl
Collecting pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.1 (from matplotlib>=2.0.0->woe)
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/6a/8a/718fd7d3458f9fab8e67186b00abdd345b639976bc7fb3ae722e1b026a50/pyparsing-2.2.0-py2.py3-none-any.whl (56kB)
    100% |████████████████████████████████| 61kB 273kB/s
Collecting pytz (from matplotlib>=2.0.0->woe)
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/3c/80/32e98784a8647880dedf1f6bf8e2c91b195fe18fdecc6767dcf5104598d6/pytz-2018.3-py2.py3-none-any.whl (509kB)
    100% |████████████████████████████████| 512kB 203kB/s
Collecting python-dateutil>=2.1 (from matplotlib>=2.0.0->woe)
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/4b/0d/7ed381ab4fe80b8ebf34411d14f253e1cf3e56e2820ffa1d8844b23859a2/python_dateutil-2.6.1-py2.py3-none-any.whl (194kB)
    100% |████████████████████████████████| 194kB 194kB/s
Collecting cycler>=0.10 (from matplotlib>=2.0.0->woe)
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/f7/d2/e07d3ebb2bd7af696440ce7e754c59dd546ffe1bbe732c8ab68b9c834e61/cycler-0.10.0-py2.py3-none-any.whl
Installing collected packages: numpy, six, pyparsing, pytz, python-dateutil, cycler, matplotlib, scipy, pandas, woe
Successfully installed cycler-0.10.0 matplotlib-2.1.2 numpy-1.14.1 pandas-0.22.0 pyparsing-2.2.0 python-dateutil-2.6.1 pytz-2018.3 scipy-1.0.0 six-1.11.0 woe-0.1.4
You are using pip version 8.1.1, however version 9.0.1 is available.
You should consider upgrading via the 'python -m pip install --upgrade pip' command.
```

via [https://www.zhihu.com/question/21653286/answer/95532074](https://www.zhihu.com/question/21653286/answer/95532074)
