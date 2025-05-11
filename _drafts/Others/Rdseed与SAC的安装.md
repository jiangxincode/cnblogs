
## Rdseed的安装

1. 下载: http://www.iris.edu/pub/programs/rdseedv5.2.tar.gz
2. 解压: tar -xzvf rdseedv5.2.tar.gz
3. 编译：

```shell
    # 在makefile中找到这几句
    CC = cc
    # for cygwin add the -D_CYGwin flag, for users of windows pcs
    CFLAGS     = -O -m32 -g -D_CYGwin
    
    # to compile rdseed as a 32-bit application
    #CFLAGS     = -O -m32 -g
    
    # 将CYGwin行注释掉，取消最下面一行的注释：
    CC = cc
    # for cygwin add the -D_CYGwin flag, for users of windows pcs
    #CFLAGS     = -O -m32 -g -D_CYGwin
    
    # to compile rdseed as a 32-bit application
    CFLAGS     = -O -m32 -g
    
    # 然后
    make clean
    make
```

4. 将编译好的rdseed文件拷贝靠bin目录下：sudo cp rdseed /usr/bin/
5. 输入rdseed即可进入。

注：64位系统下可以直接使用已编译好的文件:cp -p rdseed.rh6.linux_64 /usr/local/bin/rdseed

## SAC安装

1. 软件包可以在下面给出的网站上申请，认真填写，在平台选择处选择Linux 32 位或64位（如果有兴趣也可以选择一个source code）。注意不要图省事一次把所有包都申请了，那样管理员会专门给你发邮件要你解释的。最好使用学校邮箱或者较正规的邮箱，否则有被拒的可能。若验证通过，三个工作日内即可收到邮件。申请网址：http://www.iris.edu/forms/sac_request.htm

2. 对sac 文件压缩包直接解压，会出现sac文件夹，里面包含了多个文件夹：

```shell
    tar xvfz netcdf-3.6.3.tar.gz
    for i in *.bz2;do tar jxvf $i;done
```

3. 将整个sac 文件夹拷到某目录下（SAC 推荐安装目录为/usr/local）：

```shell
    sudo cp -r sac /usr/local
```

4. 编辑.bashrc 设置环境变量

```shell
    gedit ~/.bashrc
```

在.bashrc 的最后添加如下语句

```shell
    export SACHOME=/usr/local/sac
    export SACAUX=$SACHOME/aux
    export PATH=$SACHOME/bin:$PATH
```

5. 终端输入source ~/.bashrc 
6. 终端输入sac（注意要小写），看到版本号等信息即安装成功。