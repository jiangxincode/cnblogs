--------------------------------------------------------------------
author:jiangxin
Email:jiangxinnju@163.com
--------------------------------------------------------------------


如果大家必须在Linux环境下使用java开发应用程序，会感觉Linux下JDK和Eclipse等相关软件安装都很复杂，所以我特意写了一个脚本，这是一个在Linux下自动安装/卸载JDK和Eclipse的脚本，实现一键安装卸载，无任何额外文件产生。大家可以尝试一下。


文件包等下载地址：
http://pan.baidu.com/s/1sjArVM9
脚本能够自动识别系统是32位的还是64位的，并自动选择Jdk和Eclipse等版本。


测试环境：
Linux发行版本：Ubuntu 14.04

JDK版本：
* jdk-7u60-linux-i586（32位）
* jdk-7u60-linux-x64（64位）

Eclipse版本：
* eclipse-java-luna-R-linux-gtk（32位）
* eclipse-java-luna-R-linux-gtk-x86_64（64位）


使用时请确保此文件夹存在以下文件：
* eclipse-java-luna-R-linux-gtk.tar.gz
* eclipse-java-luna-R-linux-gtk-x86_64.tar.gz
* install.sh
* jdk-7u60-linux-i586.tar.gz
* jdk-7u60-linux-x64.tar.gz
* README
* uninstall.sh


你可以尝试修改该脚本以实现更加适合自己等功能，欢迎大家提出修改意见。
部分Linux系统会自带OpenJava，可以在安装前看看java/javac等命令是否有效。


安装脚本：

```shell
#!/bin/bash

echo "正在创建/usr/lib/jvm/目录"
sudo mkdir /usr/lib/jvm/
echo "目录/usr/lib/jvm/创建成功"

echo "正在安装JDK和Eclipse"
os_version=`uname -a`
echo $os_version
architecture="64"
echo "$os_version" | grep -q "$architecture"
if [ $? -eq 0 ]
then
	echo "您正在使用64位操作系统，为您选择64位JDK和eclipse"
	sudo tar -zxvf jdk-7u60-linux-x64.tar.gz -C /usr/lib/jvm/
	sudo chown -R jiangxin:jiangxin /usr/lib/jvm/jdk1.7.0_60
	sudo tar -zxvf eclipse-java-luna-R-linux-gtk-x86_64.tar.gz -C /usr/bin/
	sudo chown -R jiangxin:jiangxin /usr/bin/eclipse
	sudo ln -s /usr/bin/eclipse/eclipse ~/Desktop/eclipse
else
	echo "您正在使用32位操作系统，为您选择32位JDK和eclipse"
	sudo tar -zxvf jdk-7u60-linux-i586.tar.gz -C /usr/lib/jvm/
	sudo chown -R jiangxin:jiangxin /usr/lib/jvm/jdk1.7.0_60
	sudo tar -zxvf eclipse-java-luna-R-linux-gtk.tar.gz -C /usr/bin/
	sudo chown -R jiangxin:jiangxin /usr/bin/eclipse
	sudo ln -s /usr/bin/eclipse/eclipse ~/Desktop/eclipse
fi
echo "安装JDK和Eclipse成功"

echo "配置环境变量"
# touch environment  
# echo "PATH=\"$PATH:/usr/lib/jvm/jdk1.7.0_60/bin\"" >> environment
# echo "JAVA_HOME=/usr/lib/jvm/jdk1.7.0_60" >> environment
# echo "CLASSPATH=.:%JAVA_HOME%/lib/dt.jar:%JAVA_HOME%/lib/tools.jar" >> environment
# sudo mv /etc/environment /etc/environment.backup.java
# sudo mv environment /etc
# source /etc/environment

mv ~/.bashrc ~/.bashrc.backup.java
cat ~/.bashrc.backup.java >> ~/.bashrc
echo "PATH=\"$PATH:/usr/lib/jvm/jdk1.7.0_60/bin\"" >> ~/.bashrc
echo "JAVA_HOME=/usr/lib/jvm/jdk1.7.0_60" >> ~/.bashrc
echo "CLASSPATH=.:%JAVA_HOME%/lib/dt.jar:%JAVA_HOME%/lib/tools.jar" >> ~/.bashrc
source ~/.bashrc
echo "配置环境成功"

# 如果有多个java版本需要进行以下配置（包括openjdk）
echo "设置默认jdk"
sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.7.0_60/bin/java 300
sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.7.0_60/bin/javac 300
sudo update-alternatives --config java
# echo "设置默认jdk成功"


echo "测试是否安装成功"
java -version
echo "安装成功"
```

卸载脚本：

```shell
echo "正在删除相关文件"
sudo rm -rf /usr/lib/jvm/
sudo rm -rf /usr/bin/eclipse/
sudo rm -rf ~/Desktop/eclipse
wait
echo "删除相关文件成功"

echo "恢复配置文件"
# sudo rm -f /etc/environment
# sudo mv /etc/environment.backup.java /etc/environment
sudo rm /usr/bin/java /usr/bin/javac
sudo rm /etc/alternatives/java /etc/alternatives/javac
mv ~/.bashrc.backup.java ~/.bashrc
echo "恢复配置文件成功"

```