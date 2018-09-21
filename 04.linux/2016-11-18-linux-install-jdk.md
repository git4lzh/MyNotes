---
layout: post
title: "Linux安装配置JDK"
date: 2016-11-18 08:07:19
categories: [Linux,Java]
comments: true
---
## 安装JDK
1、切换至下载的目录<br>
`cd /root/downloads`

2、下载jdk(*备注：已经安装好curl工具*)<br>
`curl --progress http://download.oracle.com/otn-pub/java/jdk/8u112-b15/jdk-8u112-linux-x64.tar.gz|tar xz`

3、创建一个jvm目录存放jdk<br>
`sudo mkdir /usr/lib/jvm`

4、移动解压的jdk目录<br>
`mv jdk1.8.0_112/ /usr/lib/jvm/`

## 配置环境变量
1、编辑环境变量<br>
`sudo nano /etc/profile`

2、末尾追加内容<br>
`export JAVA_HOME=/usr/lib/jvm/jdk1.8.0_112`<br>
`export JRE_HOME=${JAVA_HOME}/jre`<br>
`export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib`<br>
`export PATH=${JAVA_HOME}/bin:$PATH`

3、设置默认jdk<br>
`sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_112/bin/java 300`<br>
`sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_112/bin/javac 300`<br>

## 测试验证
1、输入<br>
`java -version`

2、输出<br>
`root@larry-li:~/downloads# java -version`<br>
`java version "1.8.0_112"`<br>
`Java(TM) SE Runtime Environment (build 1.8.0_112-b15)`<br>
`Java HotSpot(TM) 64-Bit Server VM (build 25.112-b15, mixed mode)`<br>

表明配置成功