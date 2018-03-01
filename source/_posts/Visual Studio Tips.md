---
title: Visual Studio Tips
date: 2018-02-12 11:35:12
categories: "C"
tags:
     - vscode
description: Visual Studio Tips
toc: true
---

### 在 Visual Studio 中开发代码而无需创建项目或解决方案
在 Visual Studio 2017 中，你可以在 Visual Studio 中打开几乎任何类型的基于目录的项目的代码，而无需创建解决方案或者项目文件。 这意味着（例如，在 Git 上找到一个代码项目时）可以克隆该项目，然后在 Visual Studio 中直接打开并开始开发，而无需创建解决方案或项目。
#### 在任意位置打开代码
可以通过以下方式，在 Visual Studio 中打开代码：
* 在 Visual Studio 菜单栏上，依次选择“文件”、“打开”、“文件夹”，然后浏览到代码位置。
* 在包含该代码的文件夹的上下文（右键单击）菜单上，选择“在 Visual Studio 中打开”命令。
* 选择 Visual Studio“开始”页上的“打开文件夹”链接。
* 打开从 GitHub 存储库中克隆的代码。

![](assets/C/vs_tourtial01.png)
![](assets/C/vs_tourtial02.png)

### 调试代码
不通过项目或解决方案即可在 Visual Studio 中调试代码。 对某些语言进行调试时，可能需要在代码项目中指定一个有效的启动文件，例如脚本、可执行文件或项目。 调试代码时，Visual Studio 会首先运行此指定代码。

工具栏上“开始”按钮旁的下拉列表框中列出了 Visual Studio 检测到的所有启动项，以及你在文件夹中专门选择的项。
![](assets/C/vs_tourtial03.png)

Visual Studio 会自动识别项目，但是需要你将脚本（例如 Python 和 JavaScript）显式选择为启动项之后，项目才会出现在列表中。 此外，某些启动项（例如 MSBuild 和 CMake）可能有多个生成配置，这些生成配置会显示在运行按钮的下拉列表中。
#### 调试可执行文件
* 在 Visual Studio 菜单上，选择“调试”。 在下拉菜单上，选择该项目，或者选择想要在解决方案资源管理器中显示为启动项的项目或文件。

* 选择 F5 键开始调试。
