文章已上传到GitHub、CSDN、知乎、简书  
GitHub：https://github.com/1119204640/Minecraft-/blob/main/README.md  
CSDN：https://blog.csdn.net/weixin_46360567/article/details/122569492  
知乎：https://zhuanlan.zhihu.com/p/459142192?  
简书：https://www.jianshu.com/p/4a2094c3368e  
# Minecraft 服务器搭建过程
<!-- @[TOC](文章目录) -->
- [Minecraft 服务器搭建过程](#minecraft-服务器搭建过程)
  - [写在前面](#写在前面)
  - [更新升级系统](#更新升级系统)
  - [安装必要工具](#安装必要工具)
    - [nano](#nano)
    - [screen](#screen)
    - [wget](#wget)
    - [zip](#zip)
    - [unzip](#unzip)
  - [安装Java SDK](#安装java-sdk)
  - [在服务器创建保存文件夹](#在服务器创建保存文件夹)
  - [下载 minecraft 服务端](#下载-minecraft-服务端)
  - [运行server.jar](#运行serverjar)
  - [中断连接后，进程不被中断](#中断连接后进程不被中断)
  - [恢复 minecraft 存档](#恢复-minecraft-存档)

## 写在前面
**搭建环境：MC服务端1.16.5，HMCL客户端1.16.5，Java SE 15，服务器系统 Centos 7.6 管理员权限**  
（环境不需要与此完全一样，上述前三者匹配即可，后文会提及如何查询版本；服务器若不是管理员权限，所有命令行前都需要添加 `sudo` ）  
<br>

## 更新升级系统 
更新

    yum update -y

升级

    yum upgrade -y
<br>

## 安装必要工具
也许你不全都需要，但你最好还是跟着做吧
### nano
用于修改文本文件

    yum install nano -y
### screen
用于多窗口并发管理进程，在断开服务器后仍能继续运行进程

    yum install screen -y
### wget

    yum install wget -y
### zip
用于把文件整理到一个压缩包

    yum install zip -y
### unzip
用于压缩包的解压

    yum install unzip -y
<br>

## 安装Java SDK
版本可自行调整

    yum install java-1.8.0-openjdk -y
验证是否安装成功

    java -version
如果显示的是当前Java的版本，说明安装成功！

<br>

## 在服务器创建保存文件夹
在你喜欢的服务器位置创建即可，文件夹名：`minecraft`
（名称可以任意取）

    mkdir minecraft
进入文件夹

    cd minecraft

<br>

## 下载 minecraft 服务端
https://www.minecraft.net/en-us/download/server  
把对应版本的server.jar下载到本地，然后再上传到服务器  
<br>
然后运行server，里面的数字大小可以根据自己的服务器内存自行调整

    java -Xmx1024M -Xms1024M -jar server.jar nogui
你会发现没法运行成功，因为需要先同意 `eula.txt` ，输入下列命令行

    nano eula.txt
把里面的 `false` 改为 `true`  
然后按 **ctrl + x ,** 接着输入 `y` 按 **enter ,** 即可保存

<br>

## 运行server.jar
再次输入命令行

    java -Xmx1024M -Xms1024M -jar server.jar nogui

服务器成功运行！

<br>

## 中断连接后，进程不被中断
需要用之前安装好的 **screen** ,下述的 `mcserver` 是窗口名，可以自行任意设置

    screen -S mcserver
这样，就在新建的窗口下运行进程，防止服务器连接中断后，进程也被中断

其他有关 **screen** 的命令行常用如下：  

    screen -ls 
    列出当前所有的session

    screen -r yourname 
    回到yourname这个session
    
    screen -d yourname 
    远程detach某个session

    screen -d -r yourname
    结束当前session并回到yourname这个session

关闭或杀死窗口：`Ctrl+a k`

<br>

## 恢复 minecraft 存档
把之前保存下来的 minecraft 存档文件夹复制到当前位置  

修改 `server.properties` 文件中 `level-name = yourWorld`  

_yourWorld_ 修改为你存档文件夹的名称

<br>

---
