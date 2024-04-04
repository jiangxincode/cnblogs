# Ubuntu扩容swap文件

## 查看/卸载/删除已有swap文件

```shell
# 查看交换分区的大小和使用量
jiangxin@ubuntu11:~$ free -m
               total        used        free      shared  buff/cache   available
内存：       9815         297        6438           1        3080        9214
交换：       1897         510        1386

# 查看swap文件的位置
jiangxin@ubuntu11:~$ swapon -s
Filename                                Type            Size            Used            Priority
/swapfile                               file            1942896         522948          -2

# 卸载删除已有swap文件
jiangxin@ubuntu11:~$ sudo swapoff /swapfile
[sudo] jiangxin 的密码：
jiangxin@ubuntu11:~$ sudo rm -rf /swapfile

# 由于我们后面新增的swap文件和删除的swap文件时同名的，所以不再修改/etc/fstab文件
jiangxin@ubuntu11:~$ cat /etc/fstab
UUID=00fce965-efcd-4954-9777-14f52475b94b /               ext4    errors=remount-ro 0       1
/swapfile                                 none            swap    sw              0       0
```

## 创建/格式化/新的swap文件

```shell
# 创建一个32G的swap文件
jiangxin@ubuntu11:~$ sudo dd if=/dev/zero of=/swapfile bs=1M count=32767
记录了32767+0 的读入
记录了32767+0 的写出
34358689792字节（34 GB，32 GiB）已复制，139.379 s，247 MB/s

# 格式化创建的swap文件
jiangxin@ubuntu11:~$ sudo mkswap /swapfile
mkswap: /swapfile: insecure permissions 0644, fix with: chmod 0600 /swapfile
正在设置交换空间版本 1，大小 = 32 GiB (34358685696  个字节)
无标签， UUID=23f37fb3-b0a6-4c71-a9e0-1b4ea50a0c68

# 挂载新的swap文件，全兴提示可忽略或者按照要求整改
jiangxin@ubuntu11:~$ sudo swapon /swapfile
swapon: /swapfile：不安全的权限 0644，建议使用 0600。

# 重新查看swap分区大小
jiangxin@ubuntu11:~$ free -m
               total        used        free      shared  buff/cache   available
内存：       9815         797         135           6        8882        8703
交换：      32766           0       32766
```
