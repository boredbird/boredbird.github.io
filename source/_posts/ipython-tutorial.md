---
title: IPython Tutorial
date: 2017-10-08 18:53:12 
categories: "Python" 
tags: 
     - Python
     - IPython
description: IPython Tutorial
---

In this class, we will use [IPython notebooks](http://ipython.org/) for the
programming assignments. An IPython notebook lets you write and execute Python
code in your web browser. IPython notebooks make it very easy to tinker with
code and execute it in bits and pieces; for this reason IPython notebooks are
widely used in scientific computing.

Installing and running IPython is easy. From the command line, the following
will install IPython:

```
pip install "ipython[notebook]"
```

Once you have IPython installed, start it with this command:

```
ipython notebook
```

<!--more-->

Once IPython is running, point your web browser at http://localhost:8888 to
start using IPython notebooks. If everything worked correctly, you should
see a screen like this, showing all available IPython notebooks in the current
directory:
![](https://i.imgur.com/10DYCiX.png)

If you click through to a notebook file, you will see a screen like this:
![](https://i.imgur.com/LHUIL23.png)

An IPython notebook is made up of a number of **cells**. Each cell can contain
Python code. You can execute a cell by clicking on it and pressing `Shift-Enter`.
When you do so, the code in the cell will run, and the output of the cell
will be displayed beneath the cell. For example, after running the first cell
the notebook looks like this:
![](https://i.imgur.com/Gktm9mf.png)

Global variables are shared between cells. Executing the second cell thus gives
the following result:
![](https://i.imgur.com/Z2u3SPU.png)

By convention, IPython notebooks are expected to be run from top to bottom.
Failing to execute some cells or executing cells out of order can result in
errors:
![](https://i.imgur.com/3YovzGM.png)

After you have modified an IPython notebook for one of the assignments by
modifying or executing some of its cells, remember to **save your changes!**
![](https://i.imgur.com/GfXkc0k.png)

This has only been a brief introduction to IPython notebooks, but it should
be enough to get you up and running on the assignments for this course.
