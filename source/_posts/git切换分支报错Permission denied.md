---
title: git切换分支报错Permission denied
date: 2018-03-01 12:53:12
categories: "Python"
tags:
     - Python
     - git
description: git切换分支报错Permission denied
---
git切换分支报错，如下：
```
    maomaochong@Boredbird MINGW64 /d/Program Files/nodejs/blog (master)
    $ git checkout source
    error: cannot stat 'source/_posts': Permission denied
    error: cannot stat 'source/_posts': Permission denied
    error: cannot stat 'source/_posts': Permission denied
    error: cannot stat 'source/_posts': Permission denied
    error: cannot stat 'source/_posts': Permission denied
    error: cannot stat 'source/_posts': Permission denied
    error: cannot stat 'source/_posts': Permission denied
    error: cannot stat 'source/_posts': Permission denied
    error: cannot stat 'source/_posts': Permission denied
    error: cannot stat 'source/_posts': Permission denied
    error: cannot stat 'source/_posts': Permission denied

    maomaochong@Boredbird MINGW64 /d/Program Files/nodejs/blog (master)
    $ git checkout source
    warning: unable to rmdir .deploy_git: Directory not empty
    Checking out files: 100% (10345/10345), done.
    M       themes/next
    Switched to branch 'source'
    Your branch is up-to-date with 'origin/source'.

    maomaochong@Boredbird MINGW64 /d/Program Files/nodejs/blog (source)
    $

```

最后发现是文件占用问题，关掉后台的编辑器，顺利切换分支。
