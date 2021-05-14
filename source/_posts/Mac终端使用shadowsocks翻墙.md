经常在命令行终端下工作的码农们，SS无法正常工作。

因为在终端下不支持socks5代理，只支持http代理，这就很尴尬了。

wget、curl、git、brew等命令行工具都会变得很慢。

苹果在新系统中加入了SIP安全机制

会阻止第三方程序向系统目录内（/System，/bin，/sbin，/usr(除了/usr/local)）进行写操作，sudo也不行。

办法是先把SIP关了，等装好软件配置好后再打开SIP。或者改用其他软件。

因为懒得去把SIP关了开开了关了，找了另外一个软件privoxy。

它刚好就是安装在/usr/local内，不需要关闭SIP也可以正常使用。

privoxy 安装

安装很简单，用 brew 安装：

1
brew install privoxy
privoxy 配置

打开配置文件 /usr/local/etc/privoxy/config ：

1
vim /usr/local/etc/privoxy/config
加入下面两项配置：

1
2
listen-address 0.0.0.0:8118
forward-socks5 / localhost:1080 .
第一行设置 privoxy 监听任意IP地址的8118端口。

第二行设置本地socks5代理客户端端口。

注意不要忘了最后有一个空格和点号。
启动 privoxy

因为没有安装在系统目录内，所以启动时要打全路径。

1
sudo /usr/local/sbin/privoxy /usr/local/etc/privoxy/config
查看是否启动成功

1
netstat -na | grep 8118
privoxy 使用

在命令行终端输入如下命令，该终端即可翻墙：

1
2
export http_proxy='http://localhost:8118'
export https_proxy='http://localhost:8118'
原理是将 socks5 代理转化成 http 代理给命令行终端使用。

如果不想使用了取消即可。

1
2
unset http_proxy
unset https_proxy

