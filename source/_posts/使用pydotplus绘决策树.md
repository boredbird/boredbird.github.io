---
title: 使用pydotplus绘决策树
date: 2017-10-17 13:37:12 
categories: "Python" 
tags: 
     - Python
     - 决策树
description: 使用pydotplus绘决策树
---
首先安装`pydotplus`

`pip install pydotplus`

然后打印训练好的`clf`:

``` python

	import pydotplus
	dot_data = tree.export_graphviz(clf, out_file=None,
	                                feature_names=X_dummy.columns,
	                                class_names='target',
	                                filled=True, rounded=True,
	                                special_characters=True)
	graph = pydotplus.graph_from_dot_data(dot_data)
	graph.write_pdf("E:\\ScoreCard\\fpd30.pdf")
```

发现报错：

```

	Traceback (most recent call last):
	  File "D:\ProgramData\Anaconda2\lib\site-packages\IPython\core\interactiveshell.py", line 2881, in run_code
	    exec(code_obj, self.user_global_ns, self.user_ns)
	  File "<ipython-input-27-2c78351c7fea>", line 7, in <module>
	    graph.write_pdf("E:\\ScoreCard\\fpd30.pdf")
	  File "D:\ProgramData\Anaconda2\lib\site-packages\pydotplus\graphviz.py", line 1810, in <lambda>
	    prog=self.prog: self.write(path, format=f, prog=prog)
	  File "D:\ProgramData\Anaconda2\lib\site-packages\pydotplus\graphviz.py", line 1918, in write
	    fobj.write(self.create(prog, format))
	  File "D:\ProgramData\Anaconda2\lib\site-packages\pydotplus\graphviz.py", line 1960, in create
	    'GraphViz\'s executables not found')
	InvocationException: GraphViz's executables not found

```
提示没有找到`'GraphViz\'s executables'`:

<!--more-->

下载安装graphviz-2.38.msi 
url：http://www.graphviz.org/pub/graphviz/stable/windows/graphviz-2.38.msi

源地址下载比较慢或者打不开，可以从这里下载：
http://download.csdn.net/download/boredbird32/10025853

添加安装路径到系统Path环境变量：
D:\Program Files (x86)\Graphviz2.38\;
D:\Program Files (x86)\Graphviz2.38\bin\

重新启动Python环境发现还是报同样的错误。

点开文件`"D:\ProgramData\Anaconda2\lib\site-packages\pydotplus\graphviz.py"
` 找到 `Method 3 (Windows only)`那一段，修改里面的path为当时安装graphviz的地址。 

``` python

    # Method 3 (Windows only)
    if os.sys.platform == 'win32':

        # Try and work out the equivalent of "C:\Program Files" on this
        # machine (might be on drive D:, or in a different language)
        if 'PROGRAMFILES' in os.environ:
            # Note, we could also use the win32api to get this
            # information, but win32api may not be installed.
            path = os.path.join(
                os.environ['PROGRAMFILES'], 'ATT', 'GraphViz', 'bin'
            )
        else:
            # Just in case, try the default...
            # path = r"C:\Program Files\att\Graphviz\bin"
            path = r"D:\Program Files (x86)\Graphviz2.38\bin"

```

重启，又报错：

```

	Traceback (most recent call last):
	  File "D:\ProgramData\Anaconda2\lib\site-packages\IPython\core\interactiveshell.py", line 2881, in run_code
	    exec(code_obj, self.user_global_ns, self.user_ns)
	  File "<ipython-input-7-3735ccaa5368>", line 5, in <module>
	    graph.write_pdf("E:\\ScoreCard\\fpd30.pdf")
	  File "D:\ProgramData\Anaconda2\lib\site-packages\pydotplus\graphviz.py", line 1810, in <lambda>
	    lambda path,
	  File "D:\ProgramData\Anaconda2\lib\site-packages\pydotplus\graphviz.py", line 1918, in write
	    
	  File "D:\ProgramData\Anaconda2\lib\site-packages\pydotplus\graphviz.py", line 1960, in create
	    if self.progs is None:
	InvocationException: GraphViz's executables not found

```

继续点进去，修改源文件：
加上调试语句：

``` python

    # Method 3 (Windows only)
    if os.sys.platform == 'win32':
        print('come inside method 3')
        # Try and work out the equivalent of "C:\Program Files" on this
        # machine (might be on drive D:, or in a different language)
        if 'PROGRAMFILES' in os.environ:
            # Note, we could also use the win32api to get this
            # information, but win32api may not be installed.
            path = os.path.join(
                os.environ['PROGRAMFILES'], 'ATT', 'GraphViz', 'bin'
            )
        else:
            # Just in case, try the default...
            # path = r"C:\Program Files\att\Graphviz\bin"
            path = r"D:\Program Files (x86)\Graphviz2.38\bin"

        print(path)
        progs = __find_executables(path)
        print(progs)

        if progs is not None:

            print("Used default install location")
            return progs

    for path in (
            '/usr/bin', '/usr/local/bin',
            '/opt/local/bin',
            '/opt/bin', '/sw/bin', '/usr/share',
            '/Applications/Graphviz.app/Contents/MacOS/'):

        progs = __find_executables(path)
        if progs is not None:
            # print("Used path")
            return progs

    # Failed to find GraphViz
    return None

```

再次运行，发现：

```

	InvocationException: GraphViz's executables not found
	come inside method 3
	C:\Program Files\ATT\GraphViz\bin
	None
```

问题就出在这个path上。那干脆我们就直接在判断条件外面指定path：

```

        path = r"D:\Program Files (x86)\Graphviz2.38\bin"
        # print(path)
        progs = __find_executables(path)
        # print(progs)
```

再次运行，问题解决了：

```

	come inside method 3
	D:\Program Files (x86)\Graphviz2.38\bin
	{'twopi': 'D:\\Program Files (x86)\\Graphviz2.38\\bin\\twopi.exe', 'fdp': 'D:\\Program Files (x86)\\Graphviz2.38\\bin\\fdp.exe', 'circo': 'D:\\Program Files (x86)\\Graphviz2.38\\bin\\circo.exe', 'neato': 'D:\\Program Files (x86)\\Graphviz2.38\\bin\\neato.exe', 'dot': 'D:\\Program Files (x86)\\Graphviz2.38\\bin\\dot.exe', 'sfdp': 'D:\\Program Files (x86)\\Graphviz2.38\\bin\\sfdp.exe'}
	Used default install location
	Out[3]: 
	True

```

最后注释掉测试语句。
