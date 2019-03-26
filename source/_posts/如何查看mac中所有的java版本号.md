---
title: mac下：JDK版本相关操作
date: 2019-03-09 16:40:58
tags:
 - java
 - tip
---
查看已安装的所有JDK版本号。
修改mac默认JDK的版本。
<!-- more -->

#### 查看JDK的版本号
在mac环境下，安装完多个JDK版本后，如何查看JDK的版本号？
打开终端，输入命令：

```
$ /usr/libexec/java_home -V 

```

可以获得如下显示：

```
 Matching Java Virtual Machines (2):
    11.0.2, x86_64:	"Java SE 11.0.2"	/Library/Java/JavaVirtualMachines/jdk-11.0.2.jdk/Contents/Home
    1.8.0_201, x86_64:	"Java SE 8"	/Library/Java/JavaVirtualMachines/jdk1.8.0_201.jdk/Contents/Home

```

#### 修改当前JDK的默认版本号
当你安装了两个以上的JDK时，想要修改其默认的版本号，可以做如下操作：

1 可以先找到目录~/Library查看自己安装了哪些版本。
第一步：打开Finder（访达）。
第二步：同时按下command+🔼的箭头，到达上一级目录。
第三步：找到Library文件夹，点进去找到/Java/JavaVirtualMachines/目录。就可以看到已经安装的JDK版本号。
 <div align=center><img src="https://i.loli.net/2019/03/09/5c83a0cccee32.png" width = 100% style="margin-bottom:20px" alt="java版本" /></div>

2 修改～/.bash_profile文件。
如果想永久生效，把修改加入到profile文件中。在终端执行如下命令：

```
echo 'export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_40.jdk/Contents/Home/' >> ~/.bash_profile source ~/.bash_profile
```
注意版本号不要写错了。

Credit：
1 [https://www.jianshu.com/p/73456eca01ae](https://www.jianshu.com/p/73456eca01ae)
2 [https://blog.csdn.net/snlying/article/details/6445177](https://blog.csdn.net/snlying/article/details/6445177)