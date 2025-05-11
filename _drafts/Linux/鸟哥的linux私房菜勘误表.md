
鸟哥的Linux私房菜基础学习篇(第三版)简体中文勘误表(人民邮电出版社)
简体中文版书籍资料：
出版日期：2010年7月第3版
书籍ISBN：978-7-115-22626-6
出版社：人民邮电出版社
正文P10，0.2.2 内存，表0-2
“DDR DDRII800 64 400 800 6.4GB/s”
应改为：“DDR DDRII800 64 200 800 6.4GB/s”
P19，0.4.1 机器程序与编译程序，图0-17下面第一行
“从上面的图示我们......。鸟哥已将经程序代码(英文)写成中文，”
应改为：“从上面的图示我们......。鸟哥已经将程序代码(英文)写成中文，”
P30，1.1.2 Linux之前UNIX的历史，最后一行
“此外，Minux操作系统的开发者仅有谭宁邦教授”
应改为：“此外，Minix操作系统的开发者仅有谭宁邦教授”
P46，1.4 重点回顾
“1984年由Andrew Tannenbaum制作出Minix操作系统，”
应改为：“1984年由Andrew Tanenbaum制作出Minix操作系统，”
P46，1.4 重点回顾
“目前Linux内核的开发分为两种版本......；一种是开发中版本，如2.5.x版”
应改为：“目前Linux内核的开发分为两种版本......；一种是开发中版本的奇数版，如2.5.x版”
P55，2.2.3 X Window的学习
“Open Office(http://www.latex-project.org/)”
应改为：“Open Office(http://www.openoffice.org/)”
P160，6.5 本章练习，请问下面的目录主要放置什么数据？
“/etc/、/etc/initd、/boot、/usr/bin、/bin、/usr/sbin、/sbin、/dev、/var/log。”
应改为“/etc/、/etc/init.d、/boot、/usr/bin、/bin、/usr/sbin、/sbin、/dev、/var/log。”，并去掉前面的小方点
P200，8.1.3 Linux的Ext2文件系统(inode)，例题
“所有文件容量为：50 x 10000(bytes)= 488.3KB，但此时浪费的容量为： 4046 x 10000(bytes) = 38.6MB”
应改为“所有文件容量为：50 (bytes)x 10000 = 488.3KB，但此时浪费的容量为： 4046 (bytes) x 10000 = 38.6MB”
P203，8.1.3 Linux的Ext2文件系统(inode)，block bitmap
“同样......，此时在block bitmpap当中相对应到该block号码的标志就要修改”
应改为：“同样......，此时在block bitmap当中相对应到该block号码的标志就要修改”
P243，8.6.2 磁盘空间的浪费问题，第二个灰色框
“118  /etc   <==单位是KB”
应改为“118  /etc   <==单位是MB”
繁体中文“如果在文章內有對齊的區塊，可以使用 [ctrl]-v 進行複製/貼上/刪除的行為”
P291，10.5 重点回顾，倒数第五点
“可以使用[ctrl]-v进行复制/粘帖/删除的行为。”
P301，11.2.2 变量的显示与设置，第三行
“变量的显示就如同上面的范例，利用ehco就能够读出，”
应改为：“变量的显示就如同上面的范例，利用echo就能够读出，”
P316，11.2.8 变量内容的删除、替代与替换，第一个灰色框
“然后测试一下等号（-）的用法”
应改为：“然后测试一下减号（-）的用法”
P338，11.6.2 排序命令，本节最后一行
“就使用wc-c这个参数”
应改为：“就使用wc-m这个参数”
P354，12.2.3 基础正则表达式练习，例题四
“*(星号)：代表重复前一个0到无穷多次的意思，为组合形态”
应改为：“*(星号)：代表重复前一个字元，0到无穷多次的意思，为组合形态”
P356，12.2.4 基础正则表达式字符(characters)，表12-2，[n1-n2]
“grep -n '[0-9]' regular_express.txt”
应改为：grep -n '[A-Z]' regular_express.txt
P379，13.2.2 script的执行方式区别，图13-2 sh02.sh在父进程中运行
“sh sh02.sh在此执行”
应改为：“source sh02.sh在此执行”
P430，14.4.2 sudo，visudo与/etc/sudoers
“有趣吧……，所以这个文件就是/etc/sudoerds”
应改为“有趣吧……，所以这个文件就是/etc/sudoers”
P449，14.9 本章习题，第三个灰色框
“useradd -G youcan -s -m $username”
应改为：“useradd -G youcan -s /bin/bash -m $username”
P500，16.3.2 系统的配置文件：/etc/crontab，Tips
“/etc/init.d/crondrestart”
应改为：“/etc/init.d/crond restart”
P515，17.2.3 脱机管理问题，第二个灰色框
“[root@www ~]#exit”应在灰色框中
“如果你再次登录的话，再使用ps -l去查看你的进程，”
应改为：“如果你再次登录的话，再使用pstree去查看你的进程，”
P560，18.2.1 默认值配置文件，表18-1，per_source
“设置值：[一个数字或NULIMITED]”
应改为：“设置值：[一个数字或UNLIMITED]”
P572，18.4.3 CentOS 5.x 默认启动的服务简易说明，表18-2，xfs
“如果你不启动X窗口的话，那么这个服务可以启动。”
应改为：“如果你不启动X窗口的话，那么这个服务可以不启动。”
P572，18.5 重点回顾，倒数第三行
“而启动的方式则为/etc/init.d/xientd restart。”
应改为：“而启动的方式则为/etc/init.d/xinetd restart。”
P579，19.2.1 日志文件内容的一般格式，第四行
“某个demon执行过程老是不顺畅时；”
应改为：“设置值：某个daemon执行过程老是不顺畅时；”
P627，20.5 重点回顾，第六点
“init的配置文件为/etc/initab，”
应改为：“init的配置文件为/etc/inittab，”
P652，21.3.2 驱动USB设备，第二点
“至于USB2.0在Linux上都以Enahnced Host Controller Interface (EHCI)来驱动的。”
应改为：“至于USB2.0在Linux上都以Enhanced Host Controller Interface (EHCI)来驱动的。”
P740，25.1.3 选择备份设备，存储设备的考虑
“硬盘：/dev/hd[a-d][1-16] (IDE), /dev/sd[a-p][1-16] (SCSI/SATA)”
应改为：“硬盘：/dev/hd[a-d][1-63] (IDE), /dev/sd[a-p][1-16] (SCSI/SATA)”