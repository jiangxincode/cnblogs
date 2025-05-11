
Android版本: 4.4.2

```powershell
PS C:\Users\jiang> adb shell
shell@hwH60:/ $ su - root

# 此时输入sqlite3 发现命令无法使用
root@hwH60:/ # sqlite3
tmp-mksh: sqlite3: not found

# find一下相关文件，确定到底需要安装哪些内容，如果已经找到则不需要安装对应文件
root@hwH60:/ # find . -name "sqlite3"
root@hwH60:/ # find . -name "libsqlite.so"
root@hwH60:/ # find . -name "libsqlite_jni.so"

root@hwH60:/ # exit
shell@hwH60:/ $ exit

# 从https://files.cnblogs.com/files/jiangxinnju/sqlite3.zip处下载文件并解压。

# 将相关文件放到内置存储卡中，为什么不直接放到/system/xbin/和/system/lib/可以参考<http://www.cnblogs.com/jiangxinnju/p/8186390.html>
PS D:\> adb push sqlite3 /storage/emulated/0/
PS D:\> adb push libsqlite.so /storage/emulated/0/
PS D:\> adb push libsqlite_jni.so /storage/emulated/0/

PS D:\> adb shell
shell@hwH60:/ $ su - root

# 为什么需要重新挂载/system分区可以参考<http://www.cnblogs.com/jiangxinnju/p/8186390.html>
root@hwH60:/ # mount -o remount rw /system

# 将需要的文件从内置存储卡中转移到目标目录
root@hwH60:/ # cp /storage/emulated/0/sqlite3  /system/xbin/                              <
root@hwH60:/ # cp /storage/emulated/0/libsqlite.so  /system/lib/
root@hwH60:/ # cp /storage/emulated/0/libsqlite_jni.so  /system/lib/

# 修改对应文件的权限
root@hwH60:/ # chmod 4755 /system/xbin/sqlite3
root@hwH60:/ # chmod 0644 /system/lib/libsqlite.so
root@hwH60:/ # chmod 0644 /system/lib/libsqlite_jni.so

# 执行sqlite3命令，发现已经可以使用
root@hwH60:/ # sqlite3
SQLite version 3.7.11 2012-03-20 11:35:50
Enter ".help" for instructions
Enter SQL statements terminated with a ";"
sqlite> .exit

root@hwH60:/ # exit

# 删除内置存储卡中的文件
shell@hwH60:/ $ rm -rf /storage/emulated/0/sqlite3
shell@hwH60:/ $ rm -rf /storage/emulated/0/libsqlite.so
shell@hwH60:/ $ rm -rf /storage/emulated/0/libsqlite_jni.so

```