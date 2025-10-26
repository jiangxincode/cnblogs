## 安装Prometheus

下载地址：<https://prometheus.io/download/>

```shell
jiangxin@ubuntu11:~$ sudo mkdir /usr/local/prometheus
jiangxin@ubuntu11:~$ sudo chown -R jiangxin:jiangxin /usr/local/prometheus
jiangxin@ubuntu11:~$ cd /usr/local/prometheus/
jiangxin@ubuntu11:/usr/local/prometheus$ ls
prometheus-1.7.1.linux-amd64.tar.gz
jiangxin@ubuntu11:/usr/local/prometheus$ tar -zxvf prometheus-1.7.1.linux-amd64.tar.gz
jiangxin@ubuntu11:/usr/local/prometheus$ cd prometheus-1.7.1.linux-amd64/
```

修改：`/etc/profile`

```shell
export PROMETHEUS_HOME=/usr/local/prometheus/prometheus-1.7.1.linux-amd64
export PATH=$PATH:$PROMETHEUS_HOME
```

```shell
jiangxin@ubuntu11:/usr/local/prometheus/prometheus-1.7.1.linux-amd64$ source /etc/profile
jiangxin@ubuntu11:/usr/local/prometheus/prometheus-1.7.1.linux-amd64$ cd
```

### 启动

jiangxin@ubuntu11:~$ prometheus -config.file=${PROMETHEUS_HOME}/prometheus.yml

```log
INFO[0000] Starting prometheus (version=1.7.1, branch=master, revision=3afb3fffa3a29c3de865e1172fb740442e9d0133)  source="main.go:88"
...
```

### 查看界面
http://192.168.1.130:9090/metrics

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image189.png)

http://192.168.1.130:9090/graph

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image190.png)