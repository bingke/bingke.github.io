---
title: hadoop集群启动但不能访问50070
date: 2019-03-19 16:13:27
tags:
 - hadoop
---
最近又双叒叕搭hadoop的环境。我的问题是集群启动后，仍然无法使用localhost：50070访问结点信息。后来发现NameNode压根没起来，昨天用jps查看到的都是假象。

<!-- more -->

说正事。

首先，使用如下命令，查看是否所有进程都运行成功：

```
$ jps

```
成功的状态如下显示：

```
49697 NameNode
49777 DataNode
50116 Jps
49877 SecondaryNameNode
50076 NodeManager

```
如果你成功了，请打开你的【谷歌】浏览器，访问[localhost:50070](localhost:50070)就能成功了。为什么要用谷歌？因为我在查解决方案的时候，发现其中一个老兄用【ie】浏览器试了一天没成功，结果换成GoogleChrome浏览器问题解决。

如果你没成功，可以看一下控制台的报错信息。我的问题是hdfs-site.xml文件中，有一个设置错误。报错信息如下：

```
19/03/19 16:01:02 WARN namenode.NameNode: Encountered exception during format:
java.io.IOException: Cannot create directory /User/****/*****/hadoop-2.7.7/tmp/dfs/name/current
	at org.apache.hadoop.hdfs.server.common.Storage$StorageDirectory.clearDirectory(Storage.java:337)
	at org.apache.hadoop.hdfs.server.namenode.NNStorage.format(NNStorage.java:564)
	at org.apache.hadoop.hdfs.server.namenode.NNStorage.format(NNStorage.java:585)
	at org.apache.hadoop.hdfs.server.namenode.FSImage.format(FSImage.java:179)
	at org.apache.hadoop.hdfs.server.namenode.NameNode.format(NameNode.java:1015)
	at org.apache.hadoop.hdfs.server.namenode.NameNode.createNameNode(NameNode.java:1457)
	at org.apache.hadoop.hdfs.server.namenode.NameNode.main(NameNode.java:1582)

```

噫，这个路径看起来很出戏。原来是因为在~/hadoop-2.7.7/etc/hdfs-site.xml中的属性中，配置了一个不存在的路径。修改的地方如下：

```
    <!--把路径vlaue换成本地的name所在位置-->
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>/Users/*****/hadoop-2.7.7/tmp/dfs/name</value>
    </property>

```
修改后，保存。
重新使用命令

```
$ ./start-dfs.sh
$ ./start-yarn.sh

```

集群成功启动。再次用浏览器访问。搞定！
