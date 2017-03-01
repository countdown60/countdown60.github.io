
## 1.ubuntu安装及个性化设置
- 下载ubuntu16.04镜像，使用ultraiso制作ubuntu启动盘，然后根据指引，进行安装；

- 安装完成后，对ubuntu进行一些个性化设置，包括UI和docky等，
  1. 安装Unity Tweak Tool：
  `sudo apt-get install unity-tweak-tool `
  2. 安装GTK主题，然后设置主题：
  ```sudo add-apt-repository ppa:numix/ppa
sudo apt-get update && sudo apt-get install numix-gtk-theme ```
  3. 安装docky栏:
   `sudo apt-get install docky  `

 参见：
 [如何个性化你的Ubuntu桌面](http://os.51cto.com/art/201406/442093.htm)，
 [Ubuntu 16.04LTS安装后需要做的](http://blog.csdn.net/keith_bb/article/details/51530585).

- 因为我是thinkpad的笔记本，有小红点，所以习惯禁用触摸板。有两种方式，一种通过bios禁用，另一种是通过
安装gpointing-device-settings来设置。由于在之前使用过程中，出现gpointing-device-settings禁用
触摸板失效的情况，我此时使用bios禁用的方式`Config->Keyboard/Mouse->Touch Pad->Disabled`。
参考：[让Ubuntu完美支持Thinkpad小红点Trackpoint](http://www.linuxdiyf.com/linux/11602.html)
-主目录下的中文目录改为英文,见[中文Ubuntu主目录下的文档文件夹改回英文](http://www.linuxidc.com/Linux/2011-06/36903.htm)



## 2. 常用应用软件安装
我常用的应用软件有：搜狗输入法，wps,chrome，lantern，atom,vim，flash player等，ubuntu自带的
LibreOffice通过软件中心移除。
搜狗输入法，chrome，wps等可以在官网下载安装包，然后通过 `sudo dkpg -i softname`来安装，安装过程中出现了如下问题：
> dpkg:依赖关系问题使得 google-chrome-stable 的配置工作不能继续；

解决办法:通过`sudo apt-get -f install`来修复依赖关系，然后继续安装即可。

vim可以直接通过`sudo apt-get install vim `安装。注意，ubuntu16中，可以使用apt命令来安装。

## 3. java开发环境搭建

1. 在官网下载jdk
2. 源代码安装的软件，我习惯放在/opt目录下，所以新建java目录`sudo mkdir /opt/java`，然后移动
并解压缩到java目录下`sudo tar zxvf jdk-8u121-linux-x64.tar.gz -C /opt/java
`；
3. 配置环境变量

  通过`vim ~/.profile`来编辑‘.profile’文件，该文件是主文件下的隐藏文件，是一个个人系统变量设置文件。
```
export JAVA_HOME=/opt/java/jdk1.8.0_121
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=${JAVA_HOME}/lib:${JRE_HOME}/jre:${CLASSPATH}
export PATH=${JAVA_HOME}/bin:${PATH}
```
保存后执行`source ～/.profile`,然后通过`java -version`来查看是否配置成功
![](http://om35suyvs.bkt.clouddn.com/17-2-28/70000350-file_1488286912950_16b3b.png)

参考：[Ubuntu14配置java开发环境](http://blog.csdn.net/linruonan90/article/details/46957169)

## 4. python开发环境搭建
安装ubuntu的过程中，python环境已经有了，包含pyhon2.7和python3.5，所以这一步就省了。

## 5. mysql安装
```
sudo apt install mysql-server
sudo apt install mysql-client
sudo apt install libmysqlclient-dev
sudo apt install mysql-workbench
```
参考：[Ubuntu16.04中MySQL安装配置](http://blog.csdn.net/yancey_blog/article/details/52780357)

## 6. 虚拟机安装
```
chmod a+x VMware-Player-12.5.1-4542065.x86_64.bundle
sudo ./VMware-Player-12.5.1-4542065.x86_64.bundle
```
参考：[VMware Workstation 11图文教程](http://www.linuxidc.com/Linux/2015-01/111791.htm)
