
```shell

# 下面的例子全是以抓取eth0接口为例，如果不加”-i eth0”是表示抓取所有的接口包括lo。

# 抓取到目标主机example.com的http header头信息。-s 1024 抓取每个包的头1024 bytes (相对于默认的68Bytes)；-l 输出模式line buffer
tcpdump -i eth0 -s 1024 -l -A dst example.com

GET /somepage.php HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.2.13) Gecko/20101206 Ubuntu/10.04 (lucid) Firefox/3.6.13
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
Keep-Alive: 115
Connection: keep-alive
Cookie: uv=556903; __utma=74760.8756.122723.125824.126018.66; __utma=1.82217.512009.75006.095989.35; __utmz=1.0930.27.8.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=example; PHPSESSIONID=5C26; DWRSESSIONID=G9E5$Y4wdRi; __utmb=1.3.10.129; __utmc=1
Cache-Control: max-age=0


# 抓取http包 0x4745 为"GET"前两个字母"GE" 0x4854 为"HTTP"前两个字母"HT"
tcpdump  -XvvennSs 0 -i eth0 tcp[20:2]=0x4745 or tcp[20:2]=0x4854
 
# 抓取包含10.10.10.122的数据包 
tcpdump -i eth0 -vnn host 10.10.10.122
 
# 抓取包含10.10.10.0/24网段的数据包
tcpdump -i eth0 -vnn net 10.10.10.0/24
 
# 抓取包含端口22的数据包
tcpdump -i eth0 -vnn port 22 
 
# 抓取udp协议的数据包
tcpdump -i eth0 -vnn  udp
 
# 抓取icmp协议的数据包
tcpdump -i eth0 -vnn icmp

# 抓取arp协议的数据包
tcpdump -i eth0 -vnn arp
 
# 抓取ip协议的数据包
tcpdump -i eth0 -vnn ip
 
# 抓取源ip是10.10.10.122数据包。
tcpdump -i eth0 -vnn src host 10.10.10.122
 
# 抓取目的ip是10.10.10.122数据包
tcpdump -i eth0 -vnn dst host 10.10.10.122
 
# 抓取源端口是22的数据包
tcpdump -i eth0 -vnn src port 22
 
# 抓取源ip是10.10.10.253且目的ip是22的数据包
tcpdump -i eth0 -vnn src host 10.10.10.253 and dst port 22
                 
# 抓取源ip是10.10.10.122或者包含端口是22的数据包
tcpdump -i eth0 -vnn src host 10.10.10.122 or port 22
 
# 抓取源ip是10.10.10.122且端口不是22的数据包
tcpdump -i eth0 -vnn src host 10.10.10.122 and not port 22

# 抓取源ip是10.10.10.2且目的端口是22，或源ip是10.10.10.65且目的端口是80的数据包。
tcpdump -i eth0 -vnn \( src host 10.10.10.2 and dst port 22 \) or   \( src host 10.10.10.65 and dst port 80 \)
 
# 抓取源ip是10.10.10.59且目的端口是22，或源ip是10.10.10.68且目的端口是80的数据包。
tcpdump -i  eth0 -vnn 'src host 10.10.10.59 and dst port 22' or  ' src host 10.10.10.68 and dst port 80 '
 
# 把抓取的数据包记录存到/tmp/fill文件中，当抓取100个数据包后就退出程序。
tcpdump –i eth0 -vnn -w  /tmp/fil1 -c 100
 
# 从/tmp/fill记录中读取tcp协议的数据包
tcpdump –i eth0 -vnn -r  /tmp/fil1 tcp
 
# 从/tmp/fill记录中读取包含10.10.10.58的数据包
tcpdump –i eth0 -vnn -r  /tmp/fil1 host  10.10.10.58

```