---
title: Hadoop中DataNode没有启动解决办法
date: 2019-03-19 22:06:48
tags:
 - hadoop
---
解决Hadoop集群启动时，只有DataNode没有启动解决的问题。

<!-- more -->

当使用如下命令后，用jps查看发现，DataNode去哪里啦？

```
$ ./start-all.sh

```

DataNode不见了的罪证：

```
55680 SecondaryNameNode
55794 ResourceManager
55924 Jps
55496 NameNode
55884 NodeManager

```
因为在开始启动的时候，6项进程都在，我也没有对配置文件进行过修改。后来查到是因为使用了如下命令导致的。每一次format,namenode都会生成新的clusterID , 而datanode还是保持原来的clusterID。

```
$ hadoop namenode -format

```

我使用的解决方案：
第一步：

```
cat hadoop-2.7.7/XXXX/dfs/name/current/VERSION 
```
然后复制namenode的clusterID。
注：XXXX为在core-site.xml创建的存放临时数据的文件夹名称。

第二步：
用该clusterID把所有datanode节点机器中目录为hadoop-2.7.7/XXXX/dfs/data/current/VERSION中的clusterID替换掉。

Credit:
[https://blog.csdn.net/u013129944/article/details/78604651](https://blog.csdn.net/u013129944/article/details/78604651)
