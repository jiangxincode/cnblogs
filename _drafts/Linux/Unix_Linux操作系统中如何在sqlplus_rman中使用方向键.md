默认情况下在Unix/Linux中使用Oracle的sqlplus/rman是无法使用↑↓←→几个方向键进行操作的，要想达到Windows下使用sqlplus/rman的效果需要安装rlwrap。

rlwrap依赖readline，可以使用`rpm -q readline readline-devel` 查看系统中是否安装有readline和readline-devel，如果没有的话需要使用`yum install readline readline-devel`进行安装。如果系统不能使用yum方式安装软件，也可以按照 http://directory.fsf.org/project/readline/ 的说明进行下载、安装：

```shell
    # 根据版本差别进行对应调整
    su - root
    wget https://ftp.gnu.org/gnu/readline/readline-7.0.tar.gz
    tar -zxvf readline-7.0.tar.gz
    cd readline-7.0
    ./configure
    make
    make install
```

安装成功之后在 https://github.com/hanslub42/rlwrap 下载、安装rlwrap

```shell
    # 根据版本差别进行对应调整
    su - root
    wget https://github.com/hanslub42/rlwrap/releases/download/v0.43/rlwrap-0.43.tar.gz
    tar -zxvf rlwrap-0.43.tar.gz
    cd rlwrap-0.43
    ./configure
    make
    make install
```

安装成功之后切换到oracle用户，使用`rlwrap sqlplus user/pwd`登陆sqlplus即可在sqlplus中正常使用方向键。当然为了方便的话可以在oracle用户下的.bash_profile文件中增加如下的别名设置：

```shell
    alias sqlplus='rlwrap sqlplus'
    alias rman='rlwrap rman'
```
然后使用`source ~/.bash_porfile`刷新配置，即可直接使用`sqlplus user/pwd`登陆sqlplus。