---
title: vmware虚拟环境搭建
date: 2018-07-16 11:55:12
categories: "Python"
tags:
     - vmware
description: vmware虚拟环境搭建
---

虚拟机环境安装：
    1. VMware workstation 12 pro
    2. ubuntu-16.04-desktop-amd64.iso
    3. Boredbird,zch,zch0302

系统菜单》设置》软件和更新》切换成清华的源
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install ssh


<!--more-->

xshell连接：
1. 判断是否unbuntu安装了SSH服务：     #ps -e |grep ssh,  需要能看到sshd，否则需要安装SSH
2. 安装SSH：   # sudo apt-get install openssh-server
3. 查看是否启动ssh服务 ps -e |grep ssh
4. 启动SSH服务：  #/etc/init/ssh start
5. 查看Ubuntu本机IP：ifconfig -a
6. 在虚拟机上测试是否能成功登陆：    #ssh -l   用户名  本机IP

    root@ubuntu:/# ssh -l zch 192.168.171.128
7. xshell连接配置


Ubuntu虚拟机python环境：
1. 在宿主机中将Anaconda2-4.3.1-Linux-x86_64.sh放在VMware的共享文件夹
2. Ubuntu中进入目录 cd /mnt/hgfs/
3. Anaconda2安装：<br/><del/> sudo sh Anaconda2-4.3.1-Linux-x86_64.sh </del></br><br/>bash Anaconda2-4.3.1-Linux-x86_64.sh</br>

    ```
    zch@ubuntu:/mnt/hgfs/shareVM$ sudo sh Anaconda2-4.3.1-Linux-x86_64.sh
    [sudo] password for zch:
    Anaconda2-4.3.1-Linux-x86_64.sh: 16: Anaconda2-4.3.1-Linux-x86_64.sh: 0: not found
    Anaconda2-4.3.1-Linux-x86_64.sh: 61: Anaconda2-4.3.1-Linux-x86_64.sh: 0: not found
    Anaconda2-4.3.1-Linux-x86_64.sh: 75: Anaconda2-4.3.1-Linux-x86_64.sh: Syntax error: word unexpected (expecting ")")

    此时共享文件夹中的可执行文件sh有个后缀*星号
    zch@ubuntu:/mnt/hgfs/shareVM$ ll
    total 473123
    drwxrwxrwx 1 root root         0 Mar 24 02:09 ./
    dr-xr-xr-x 1 root root      4192 Mar 24 02:16 ../
    -rwxrwxrwx 1 root root 484472684 Jun 13  2017 Anaconda2-4.3.1-Linux-x86_64.sh*
    zch@ubuntu:/mnt/hgfs/shareVM$ ls -F
    Anaconda2-4.3.1-Linux-x86_64.sh*

    chmod -x Anaconda2-4.3.1-Linux-x86_64.sh
    ```
4. [Linux下系统自带python和Anaconda切换](https://blog.csdn.net/zhangxinyu11021130/article/details/64125058)
    ```
    root@ubuntu:~# vim .bashrc
    添加：
    export PATH="/root/anaconda2/bin:$PATH"
    root@ubuntu:~# source ~/.bashrc
    效果如下：
    root@ubuntu:~# vim .bashrc
    root@ubuntu:~# source ~/.bashrc
    root@ubuntu:~# python
    Python 2.7.13 |Anaconda 4.3.1 (64-bit)| (default, Dec 20 2016, 23:09:15)
    [GCC 4.4.7 20120313 (Red Hat 4.4.7-1)] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    Anaconda is brought to you by Continuum Analytics.
    Please check out: http://continuum.io/thanks and https://anaconda.org
    >>>
    ```
5. 设置Ubuntu允许root用户ssh登陆
    ```
    1. 修改root密码
    root@ubuntu:~/anaconda2/bin# sudo passwd root
    Enter new UNIX password:
    Retype new UNIX password:
    passwd: password updated successfully
    2. 修改配置文件
    root@ubuntu:~/anaconda2/bin# vim /etc/ssh/sshd_config
    将原来：
    # Authentication:  
    LoginGraceTime 120  
    PermitRootLogin prohibit-password  
    StrictModes yes  
    替换为：
    # Authentication:  
    LoginGraceTime 120  
    #PermitRootLogin prohibit-password  
    PermitRootLogin yes  
    StrictModes yes
    3.重启ssh服务
    root@ubuntu:~/anaconda2/bin# sudo service ssh restart
    ```

6. pycharm中连接Ubuntu的python环境
    ![pycharm add remote](assets/20180324182804.png)

pip 安装：

    root@ubuntu:~# sudo apt-get install python-pip


conda设置国内镜像:
    # 添加Anaconda的TUNA镜像
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
    # TUNA的help中镜像地址加有引号，需要去掉

    # 设置搜索时显示通道地址
    conda config --set show_channel_urls yes



[pytorch](http://pytorch.org/previous-versions/)安装与测试：

    root@ubuntu:~# conda install pytorch torchvision cuda80 -c soumith
    问题:
    conda: command not found
    解决办法：立即生效环境变量
    root@ubuntu:~/anaconda2/bin# source ~/.bashrc
    root@ubuntu:~/anaconda2/bin# conda list

    问题：
    在终端下输入官网给出的命令，安装pytorch、torchvision
    由于被墙的原因无法进行选择，本文采用shadowsocks代理
    解决办法：[采用shadowsocks代理](https://blog.csdn.net/h406395933/article/details/75200540)
    1. 添加ppa源：
    $ sudo add-apt-repository ppa:hzwhuang/ss-qt5
    $ sudo apt-get update
    $ sudo apt-get install shadowsocks-qt5
    2. 启动shadowsocks
    点击连接-添加-手动进行配置

[torch-0.3.0.post4-cp27-cp27mu-linux_x86_64.whl下载](http://download.pytorch.org/whl/cu80/torch-0.3.0.post4-cp27-cp27mu-linux_x86_64.whl)


tensorflow安装：

    sudo pip install --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.9.0-cp27-none-linux_x86_64.whl

[tensorflow中文教程](http://www.tensorfly.cn/tfdoc/get_started/basic_usage.html)

[crf++](https://taku910.github.io/crfpp/)安装与测试：

[crfpp downloads](https://drive.google.com/drive/folders/0B4y35FiV1wh7fngteFhHQUN2Y1B5eUJBNHZUemJYQV9VWlBUb3JlX0xBdWVZTWtSbVBneU0)


1. [crf++ 0.58 下载](https://download.csdn.net/download/wds2006sdo/9720302)
2. [crf++ 安装](https://blog.csdn.net/u010004460/article/details/77198389)
3. import CRFPP报错：

    [解决办法](https://blog.csdn.net/u010004460/article/details/77198389)：
    <br/>ln -s /usr/local/lib/libcrfpp.so.0 /usr/lib/ </br>
