---
title: python的-m参数
date: 2017-10-09 14:53:12 
categories: "Python" 
tags: 
     - Python
description: python的-m参数
---
# 单个文件
## 创建测试文件：

`E:\Code\ScoreCard>`路径下创建`testm.py`文件，内容如下：
``` python

	import sys
	print(sys.path)
	
	if __name__ == "__main__":
	    print ('This is main of module ')

```

## 在终端上运行：
![](https://i.imgur.com/UGJcAPs.png)

## 查看帮助文档：
![](https://i.imgur.com/GXYAjii.png)

```
	-m mod : run library module as a script (terminates option list)
```

# 创建模块测试-m作用
## 文档目录结构：
![](https://i.imgur.com/z84nr20.png)

<!--more-->

`E:\Code\ScoreCard\package1>`路径下创建`testm1.py`文件，内容如下：
``` python

	import sys
	print(sys.path)
	
	if __name__ == "__main__":
	    print ('This is main of module 1')

```

`E:\Code\ScoreCard\package2>`路径下创建`testm2.py`文件，内容如下：
``` python

	import sys
	from package1 import testm1
	print(sys.path)
	
	if __name__ == "__main__":
	    print ('This is main of module 2')

```

## 在终端上测试,效果如下:

![](https://i.imgur.com/oRAASuZ.png)

![](https://i.imgur.com/l5oRrHi.png)

# 结论
```

	-m 是把模块当作脚本来启动；
	直接启动是把run.py文件，所在的目录放到了sys.path属性中，见sys.path输出列表的第一个；
	模块启动是把你输入命令的目录（也就是当前路径），放到了sys.path属性中，见sys.path输出列表的第一个；
	
	当需要启动的py文件引用了一个模块。你需要注意：在启动的时候需要考虑sys.path中有没有你import的模块的路径！这个时候，到底是使用直接启动，还是以模块的启动？目的就是把import的那个模块的路径放到sys.path中。
```

**参考**
[here](http://www.cnblogs.com/xueweihan/p/5118222.html)
