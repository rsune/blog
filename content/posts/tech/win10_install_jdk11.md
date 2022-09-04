---
title: "Windows10环境下安装JDK11" #标题
date: 2022-02-25T16:49:00+08:00 #创建时间
lastmod: 2022-09-04T17:22:26+08:00 #更新时间
author: ["Sunrise"] #作者
categories: 
- "教程"
tags: 
- "Java"
description: "" #描述
weight: 1# 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true #是否展示评论
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: false # 底部不显示分享栏
showbreadcrumbs: true #顶部显示当前路径
cover:
  image: "/posts/tech/win10_install_jdk11/cover.png" #封面路径
  caption: "" #图片底部描述
  alt: ""
  relative: false
---

## 一、前言

​	重装系统不久，再次安装JDK。本篇笔记记录了此次安装流程，以省去以后查找资料的麻烦。尽管Oracle已经于2021年9月份推出了最新的JDK17，但考虑到适配性等因素，选用了更为稳定的JDK11。

*操作环境：*

​	Windows 10专业版，版本号21H2，操作系统内部版本19044.1526。

## 二、内容

### 1.下载JDK

​	进入[官网](https://www.oracle.com/java/technologies/downloads/#java11)下载，有两种版本，此处选择了64位免安装版（.zip），解压后配置环境变量即可使用。

![1.png](/posts/tech/win10_install_jdk11/1.png)

*注：*下载需要登录Oracle账号，如果没有账号的话也可以根据本文**总结**给出的分享链接完成下载。

### 2.下载并解压至合适位置

​	将下载好的文件解压，并将其移动到合适的位置，此处我将解压后的文件夹移动到了D盘下的App目录中。

![2.png](/posts/tech/win10_install_jdk11/2.png)

### 3.配置环境变量

1. 进入**Windows设置**中的**系统**，在**关于**栏点击**高级系统设置**。

![3.png](/posts/tech/win10_install_jdk11/3.png)

![4.png](/posts/tech/win10_install_jdk11/4.png)

2. 点击系统属性面板的*环境变量*，然后点击**系统变量**下的**新建**来创建一个新的系统变量。

   *注：***用户变量**只对当前用户有效，**系统变量**对所有用户有效，两者的详细区别可参考[知乎回答](https://zhuanlan.zhihu.com/p/93719752)。

![5.png](/posts/tech/win10_install_jdk11/5.png)

​	在新建系统变量面板的变量名一栏中填入**JAVA_HOME**，然后点击浏览目录，定位到JDK安装目录。

![6.png](/posts/tech/win10_install_jdk11/6.png)

*注：*也可以直接复制该文件夹路径填入**变量值**。

![7.png](/posts/tech/win10_install_jdk11/7.png)

![8.png](/posts/tech/win10_install_jdk11/8.png)

效果：

![9.png](/posts/tech/win10_install_jdk11/9.png)

3. 编辑**Path**系统变量，添加**%JAVA_HOME%\bin**。

   *注：***%JAVA_HOME%**代表系统变量**JAVA_HOME**的值，实际上是将**D:\App\jdk-11.0.14\bin**文件夹添加到**Path**变量中，用于系统扫描其中的可执行文件。

![10.png](/posts/tech/win10_install_jdk11/10.png)

4. 点击确定，保存修改。

![11.png](/posts/tech/win10_install_jdk11/11.png)

### 4.检验效果

1. 进入CMD命令行

   按**Win+R**唤出**运行**工具，输入cmd后点确定即可。

![12.png](/posts/tech/win10_install_jdk11/12.png)

![13.png](/posts/tech/win10_install_jdk11/13.png)

2. 输入  **path**  命令，查看环境变量。

   如果之前设置的结果正确出现，则说明系统变量配置正确。

![14.png](/posts/tech/win10_install_jdk11/14.png)

3. 分别输入以下命令，观察结果

```
java			//运行Java程序
javac			//编译Java源程序（*.java）
java --version	 //查看Java版本
```

![15.png](/posts/tech/win10_install_jdk11/15.png)

![16.png](/posts/tech/win10_install_jdk11/16.png)

![17.png](/posts/tech/win10_install_jdk11/17.png)

如果出现上图所示结果，说明JDK配置成功。

### 5.简单使用

1. 在合适的位置新建一个文本文件，命名为Test.txt。（此处放置于D盘根目录下）

2. 使用记事本打开，写入以下测试代码。

   ```java
   //Test.java
   
   public class Test{
       public static void main(String args[]){
           System.out.println("Hello World!");
       }
   }
   ```

3. 将文件名改为Test.java。

   *注：*如果文件默认没有显示后缀名可以点击资源管理器上的**查看**，修改后缀可见性设置

   ![18.png](/posts/tech/win10_install_jdk11/18.png)

4. 运行cmd命令行程序，定位到该文件所在目录。

   *注：*在文件所在目录的搜索框内输入**cmd**后回车，可直接在该目录下运行命令行程序。

   ![19.png](/posts/tech/win10_install_jdk11/19.png)

   ![20.png](/posts/tech/win10_install_jdk11/20.png)

   可在命令行内执行  **dir**  命令查看该目录下的所有文件。

   ![21.png](/posts/tech/win10_install_jdk11/21.png)

5. 执行命令  **javac Test.java**  编译Java源程序

   编译完成后目录中会出现编译完成的字节码文件**Test.class**。

   ![22.png](/posts/tech/win10_install_jdk11/22.png)

6. 执行命令  **java Test**  运行该字节码文件，如果输出  **Hello World！**  说明JDK能正常使用。

   **注：**java命令后紧跟的文件名**不需要包含后缀**，否则会提示无法找到。

   ![23.png](/posts/tech/win10_install_jdk11/23.png)

## 三、总结

​	这次自己重装系统后独立完成了JDK11的安装，同时记录了整个流程，巩固了记忆。以前都是运行可执行文件（如**jdk-11.0.14_windows-x64_bin.exe**）来完成安装，而这次选用了解压安装的方式完成，可定制性更高。电脑上可以同时存在多个版本的JDK，只需要在使用的时候修改**JAVA_HOME**系统变量的值即可，更为方便:smile:。

>相关资源链接：
>
>* JDK11：https://www.123pan.com/s/M6VA-2vAIh，提取码:XnGA
>
>关于**classpath**的问题可参考廖雪峰老师的文章：[classpath和jar](https://www.liaoxuefeng.com/wiki/1252599548343744/1260466914339296)。





