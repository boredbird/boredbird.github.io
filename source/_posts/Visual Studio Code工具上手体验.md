---
title: Visual Studio Code工具上手体验
date: 2017-10-17 13:37:12 
categories: "Python" 
tags: 
     - Python
     - vscode
description: Visual Studio Code工具上手体验
---
下载安装Visual Studio Code,地址：https://code.visualstudio.com/Download

在VSCode内安装c++插件：
打开vscode，Ctrl+P之后输入`ext install c++`

![](assets/C/vscode1.png)

弹出：

```

	扩展：商店   错误
```

不用管它，重新再来一次，Ctrl+P之后输入`ext install c++`

安装第一个官方的。

![](assets/C/vscode2.png)

重启vscode。然后发现重新启动，vscode开始自动下载插件依赖。
依赖自动下载安装完成。

<!--more-->

![](assets/C/vscode3.png)

抬头，提示reload。

查看本机`gcc`环境：

```

	E:\Code\solar-correlation-map>gcc -v
	Using built-in specs.
	COLLECT_GCC=gcc
	COLLECT_LTO_WRAPPER=D:/TDM-GCC-64/bin/../libexec/gcc/x86_64-w64-mingw32/5.1.0/lto-wrapper.exe
	Target: x86_64-w64-mingw32
	Configured with: ../../../src/gcc-5.1.0/configure --build=x86_64-w64-mingw32 --enable-targets=all --enable-languages=ada,c,c++,fortran,lto,objc,obj-c++ --enable-libgomp --enable-lto --enable-graphite --enable-cxx-flags=-DWINPTHREAD_STATIC --disable-build-with-cxx --disable-build-poststage1-with-cxx --enable-libstdcxx-debug --enable-threads=posix --enable-version-specific-runtime-libs --enable-fully-dynamic-string --enable-libstdcxx-threads --enable-libstdcxx-time --with-gnu-ld --disable-werror --disable-nls --disable-win32-registry --prefix=/mingw64tdm --with-local-prefix=/mingw64tdm --with-pkgversion=tdm64-1 --with-bugurl=http://tdm-gcc.tdragon.net/bugs
	Thread model: posix
	gcc version 5.1.0 (tdm64-1) 

```

新建文件夹，在文件夹内新建文件hello.cpp：
```

	\#include <iostream>
	using namespace std;
	int main()
	{
	    int a = 0;
	    cout<<a;
	    return 0;
	}
```

按下F5，启动调试，提示需要配置。
将`launch.json`的文件内容替换成如下：

```

	{
	    "version": "0.2.0",
	    "configurations": [
	        {
	            "name": "C++ Launch (GDB)",                 // 配置名称，将会在启动配置的下拉菜单中显示
	            "type": "cppdbg",                           // 配置类型，这里只能为cppdbg
	            "request": "launch",                        // 请求配置类型，可以为launch（启动）或attach（附加）
	            "launchOptionType": "Local",                // 调试器启动类型，这里只能为Local
	            "targetArchitecture": "x86",                // 生成目标架构，一般为x86或x64，可以为x86, arm, arm64, mips, x64, amd64, x86_64
	            "program": "${file}.exe",                   // 将要进行调试的程序的路径
	            // "miDebuggerPath":"c:\\MinGW\\bin\\gdb.exe", // miDebugger的路径，注意这里要与MinGw的路径对应
	            "miDebuggerPath":"D:\\TDM-GCC-64\\bin\\gdb.exe",
	            "args": ["blackkitty",  "1221", "# #"],     // 程序调试时传递给程序的命令行参数，一般设为空即可
	            "stopAtEntry": false,                       // 设为true时程序将暂停在程序入口处，一般设置为false
	            "cwd": "${workspaceRoot}",                  // 调试程序时的工作目录，一般为${workspaceRoot}即代码所在目录
	            "externalConsole": true,                    // 调试时是否显示控制台窗口，一般设置为true显示控制台
	            "preLaunchTask": "g++"　　                  // 调试会话开始前执行的任务，一般为编译程序，c++为g++, c为gcc
	        }
	    ]
	}
```

**注意miDebuggerPath要与MinGw的路径对应 **
替换后保存，然后切换至hello.cpp，按F5进行调试，此时会弹出一个信息框要求你配置任务运行程序，点击它~ 

选择任务运行程序，点击Others，跳出tasks.json的配置文件。 
替换成如下代码:

```

	{
	    "version": "0.1.0",
	    "command": "g++",
	    "args": ["-g","${file}","-o","${file}.exe"],    // 编译命令参数
	    "problemMatcher": {
	        "owner": "cpp",
	        "fileLocation": ["relative", "${workspaceRoot}"],
	        "pattern": {
	            "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning|error):\\s+(.*)$",
	            "file": 1,
	            "line": 2,
	            "column": 3,
	            "severity": 4,
	            "message": 5
	        }
	    }
	}
```
保存一下，然后切换至hello.cpp，再次按F5启动调试:

控制台输出：

```

	=thread-group-added,id="i1"
	GNU gdb (GDB) 7.9.1
	Copyright (C) 2015 Free Software Foundation, Inc.
	License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
	This is free software: you are free to change and redistribute it.
	There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
	and "show warranty" for details.
	This GDB was configured as "x86_64-w64-mingw32".
	Type "show configuration" for configuration details.
	For bug reporting instructions, please see:
	<http://www.gnu.org/software/gdb/bugs/>.
	Find the GDB manual and other documentation resources online at:
	<http://www.gnu.org/software/gdb/documentation/>.
	For help, type "help".
	Type "apropos word" to search for commands related to "word".
	=cmd-param-changed,param="pagination",value="off"
	[New Thread 16288.0x3d10]
	Breakpoint 1, main () at e:\Code\C_playground\hello.cpp:5
	5	    int a = 0;
	[Inferior 1 (process 16288) exited normally]
	The program 'e:\Code\C_playground\hello.cpp.exe' has exited with code 0 (0x00000000).

```

文档目录如下：

![](assets/C/vscode4.png)


