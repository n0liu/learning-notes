# linux服务器安装nginx及使用

Nginx在个人的使用之后，感觉非常的方便，所以在这里给出自己安装配置方案。它是一款高性能的 Web和 反向代理 服务器，也是一个 IMAP/POP3/SMTP 代理服务器。负载均衡是个不错的选择。

我的linux服务器是阿里云的 CentOS 7.4 64位，下面是安装过程

### 😀 **第一步：先安装PCRE pcre-devel 和Zlib，再配置nginx的时候会用到**

PCRE(Perl Compatible Regular Expressions) 是一个Perl库，包括 perl 兼容的正则表达式库。nginx 的 http 模块使用 pcre 来解析正则表达式，所以需要在 linux 上安装 pcre 库，pcre-devel 是使用 pcre 开发的一个二次开发库。nginx也需要此库。命令：

```bash
yum install -y pcre pcre-devel
```

![](https://img2018.cnblogs.com/blog/1470384/201904/1470384-20190409121542122-2035469450.png)

zlib 库提供了很多种压缩和解压缩的方式， nginx 使用 zlib 对 http 包的内容进行 gzip ，所以需要在Centos 上安装 zlib 库。

```bash
yum install -y zlib zlib-devel
```

![](https://img2018.cnblogs.com/blog/1470384/201904/1470384-20190409121703911-1003096243.png)

安装好这两个之后就可以安装nginx了，但是如果安装的时候有问题的话可能需要安装GCC和OpenSSL以下提供命令

```bash
yum install gcc-c++ yum install -y openssl openssl-devel
```

### 😃 **第二步：安装nginx 1.14.0**

```bash
wget -c https://nginx.org/download/nginx-1.14.0.tar.gz
```

解压并进入nginx目录

```bash
tar -zxvf nginx-1.14.0.tar.gz
cd nginx-1.14.0
```

使用nginx的默认配置

```bash
./configure
```

编译安装

```bash
make
make install
```

查找安装路径：

```bash
whereis nginx
```

![](https://img2018.cnblogs.com/blog/1470384/201904/1470384-20190409141710895-1972575936.png)

进入`sbin`目录，可以看到有一个可执行文件`nginx`，直接./执行就OK了。

运行起来之后访问服务器ip，可以看到nginx的欢迎页面

![](https://img2018.cnblogs.com/blog/1470384/201904/1470384-20190409141912922-232230531.png)

![](https://img2018.cnblogs.com/blog/1470384/201904/1470384-20190409151623454-1676344291.png)

> &#x20;**这里提几点需要注意的地方**

1.安装好启动好后无法访问到页面

查看是否安装好

```bash
ps -ef|grep nginx
```

![](https://img2018.cnblogs.com/blog/1470384/201904/1470384-20190409152151927-909034755.png)

如果如上图有nginx的进程说明启动好了这个时候如果无法访问nginx页面可以先查看一下你服务器的安全组策略**是否有启用80端口**

下图表示已开启

![](https://img2018.cnblogs.com/blog/1470384/201904/1470384-20190409152428264-647363183.png)

如果启用之后还是无法访问需要查看nginx的配置文件`nginx.conf`

**先查找自己的**\*\*`nginx`\*\***安装目录**

```bash
whereis nginx
```

![](https://img2018.cnblogs.com/blog/1470384/201904/1470384-20190409152712344-1875541177.png)

目录在`/usr/local/nginx`中，进入`sbin`文件夹下面发现有一个`nginx`的可执行文件

在`sbin`中可以执行下面这个语句查询自己使用的`nginx.conf`在哪个位置，同时这个语句也可以验证你的`nginx.conf`文件是否是正确的。正确的格式会提示`test is successful`

```bash
./nginx -t
```

![](https://img2018.cnblogs.com/blog/1470384/201904/1470384-20190409153042438-1377542008.png)

找到这个配置文件目录在`/usr/local/nginx/conf`下

我们编辑里面的映射路径

![](https://img2018.cnblogs.com/blog/1470384/201904/1470384-20190409153506109-1419287243.png)

把这个路径改为你的文件存放路径

![](https://img2018.cnblogs.com/blog/1470384/201904/1470384-20190409153602121-86768224.png)

这样的话基本没有问题了，有其他问题也可以说出来一起探讨。

最后是nginx的一些基本命令，有一些已经在前面提到了，这里也一并列出

**启动**

启动代码格式：nginx安装目录地址 -c nginx配置文件地址

```bash
/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
```

**停止**

nginx的停止有三种方式

**从容停止**

```bash
ps -ef|grep nginx
```

![](https://img2018.cnblogs.com/blog/1470384/201904/1470384-20190409154711813-1966650821.png)

杀死进程

```bash
kill -QUIT 3905
```

**快速停止**

```abap
kill -TERM 3905
```

或者

```bash
kill -INT 3905
```

**强制停止**

```bash
pkill -9 nginx
```

**重启**

方法一：进入`nginx`可执行目录`sbin`下，输入命令`./nginx -s reload` 即可

![](https://img2018.cnblogs.com/blog/1470384/201904/1470384-20190409155547898-1115398652.png)

方法二：查找当前`nginx`进程号，然后输入命令：`kill -HUP`进程号 实现重启

![](https://img2018.cnblogs.com/blog/1470384/201904/1470384-20190409155908331-1050350400.png)
