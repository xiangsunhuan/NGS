## wget和curl的基本用法

`wget` 和 `curl` 都可以下载内容。

由于这两者都是命令行工具，它们都被设计成可脚本化。`wget` 和 `curl` 都可以写进你的 Bash 脚本 ，自动与新内容交互，下载所需内容。
### curl 和 wget 区别：
1. curl 是 libcurl 这个库支持的，wget 是一个纯粹的命令行命令。
2. curl 在指定要下载的链接时能够支持 URL 的序列或集合，而 wget 则不能这样;
3. wget 支持 递归下载，而 curl 则没有这个功能。
4. curl 由于可自定义各种请求参数，所以在 模拟 web 请求 方面更擅长；cURL是一个多功能工具。当然，它可以下载网络内容，但同时它也能做更多别的事情。cURL 技术支持库是：libcurl。这就意味着你可以基于 cURL 编写整个程序，允许你基于 libcurl 库中编写图形环境的下载程序，访问它所有的功能。cURL 宽泛的网络协议支持可能是其最大的卖点。cURL 支持访问 HTTP 和 HTTPS 协议，能够处理 FTP 传输。它支持 LDAP 协议，甚至支持 Samba 分享。实际上，你还可以用 cURL 收发邮件。cURL 也有一些简洁的安全特性。cURL 支持安装许多 SSL/TLS 库，也支持通过网络代理访问，包括 SOCKS。这意味着，你可以越过 Tor 来使用cURL。cURL 同样支持让数据发送变得更容易的 gzip 压缩技术。
5. wget 由于支持 ftp 和 Recursive(递归)下载， 所以在下载文件方面更擅长。wget 简单直接。这意味着你能享受它超凡的下载速度。wget 是一个独立的程序，无需额外的资源库，更不会做其范畴之外的事情。wget 是专业的直接下载程序，支持递归下载。同时，它也允许你下载网页中或是 FTP 目录中的任何内容。wget 拥有智能的默认设置。它规定了很多在常规浏览器里的事物处理方式，比如 cookies 和重定向，这都不需要额外的配置。
类比的话，可以把 curl 看做是一个精简的命令行网页浏览器。它支持几乎你能想到的所有协议，curl 宽泛的网络协议支持可能是其最大的卖点（curl支持更多的协议。curl supports FTP, FTPS, HTTP, HTTPS, SCP, SFTP, TFTP, TELNET, DICT, LDAP, LDAPS, FILE, POP3, IMAP, SMTP and RTSP at the time of this writing. Wget supports HTTP, HTTPS and FTP.）。curl 支持访问 HTTP 和 HTTPS 协议，能够处理 FTP 传输。它支持 LDAP 协议，甚至支持 Samba 分享。实际上，你还可以用 cURL 收发邮件。curl 可以交互访问几乎所有在线内容。唯一和浏览器不同的是，curl 不会渲染接收到的相应信息。

这个比较得看实际用途。如果你想快速下载并且没有担心参数标识的需求，那你应该使用轻便有效的 wget。如果你想做一些更复杂的使用，直觉告诉你，你应该选择 cRUL。

## 一、wget 使用实例
### 1、使用 wget 下载单个文件
以下的例子是从网络下载一个文件并保存在当前目录
```
wget http://cn.wordpress.org/wordpress-3.1-zh_CN.zip
```
在下载的过程中会显示进度条，包含（下载完成百分比，已经下载的字节，当前下载速度，剩余下载时间）。

### 2、使用 wget -O 下载并以不同的文件名保存
wget默认会以最后一个符合”/”的后面的字符来命令，对于动态链接的下载通常文件名会不正确。
错误：下面的例子会下载一个文件并以名称download.php?id=1080保存
```
wget http://www.centos.bz/download?id=1
```
即使下载的文件是zip格式，它仍然以download.php?id=1080命令。
正确：为了解决这个问题，我们可以使用参数-O来指定一个文件名：
```
wget -O wordpress.zip http://www.centos.bz/download.php?id=1080
```
### 3、使用 wget --limit -rate 限速下载
当你执行wget的时候，它默认会占用全部可能的宽带下载。但是当你准备下载一个大文件，而你还需要下载其它文件时就有必要限速了。
```
wget –limit-rate=300k http://cn.wordpress.org/wordpress-3.1-zh_CN.zip
```
### 4、使用 wget -c 断点续传
当文件特别大或者网络特别慢的时候，往往一个文件还没有下载完，连接就已经被切断，此时就需要断点续传。
wget的断点续传是自动的，只需要使用 -c 参数。使用断点续传要求服务器支持断点续传。
例如： `wget -c http://the.url.of/incomplete/file`
-t 参数表示重试次数，例如需要重试100次，那么就写-t 100，如果设成-t 0，那么表示无穷次重试，直到连接成功。
-T 参数表示超时等待时间，例如-T 120，表示等待120秒连接不上就算超时。

### 5、使用 wget -b 后台下载
对于下载非常大的文件的时候，我们可以使用参数-b进行后台下载。
```
wget -b http://cn.wordpress.org/wordpress-3.1-zh_CN.zip
Continuing in background, pid 1840.
Output will be written to `wget-log’.
你可以使用以下命令来察看下载进度

tail -f wget-log
```

### 6、使用代理服务器(proxy) 和 伪装代理(user-agent)名称下载


如果用户的网络需要经过代理服务器，那么可以让 wget 通过代理服务器进行文件的下载。
此时需要在当前用户的目录下创建一个 .wgetrc 文件。

文件中可以设置代理服务器：
```
http-proxy = 111.111.111.111:8080
ftp-proxy = 111.111.111.111:8080
```
分别表示http的代理服务器和ftp的代理服务器。

如果代理服务器需要密码，则使用这两个参数：
```
–proxy-user=USER      设置代理用户
–proxy-passwd=PASS    设置代理密码
```
使用参数 `–proxy=on/off` 使用或者关闭代理。

### 7、使用 wget --spider 测试下载链接
当你打算进行定时下载，你应该在预定时间测试下载链接是否有效。我们可以增加–spider参数进行检查。
```
wget –spider URL
如果下载链接正确，将会显示

wget –spider URL
Spider mode enabled. Check if remote file exists.
HTTP request sent, awaiting response… 200 OK
Length: unspecified [text/html]
Remote file exists and could contain further links,
but recursion is disabled — not retrieving.
这保证了下载能在预定的时间进行，但当你给错了一个链接，将会显示如下错误

wget –spider url
Spider mode enabled. Check if remote file exists.
HTTP request sent, awaiting response… 404 Not Found
Remote file does not exist — broken link!!!
```
你可以在以下几种情况下使用spider参数：

定时下载之前进行检查
间隔检测网站是否可用
检查网站页面的死链接


### 8、使用 wget --tries 增加重试次数
如果网络有问题或下载一个大文件也有可能失败。wget默认重试20次连接下载文件。如果需要，你可以使用–tries增加重试次数。
```
wget –tries=40 URL
```
### 9、使用 wget -i 下载多个文件 （批量下载）

如果有多个文件需要下载，那么可以生成一个文件，把每个文件的 URL 写一行。

例如，生成文件 download.txt，然后用命令：`wget -i download.txt`

这样就会把download.txt里面列出的每个URL都下载下来。（如果列的是文件就下载文件，如果列的是网站，那么下载首页）


### 10、使用 wget -r -A 下载指定格式文件
可以在以下情况使用该功能

下载一个网站的所有图片
下载一个网站的所有视频
下载一个网站的所有PDF文件
wget -r -A.pdf url

### 11、下载整个 http 或者  wget FTP 下载
```
wget http://place.your.url/here
```
这个命令可以将 http://place.your.url/here 首页下载下来。
使用 `-x `会强制建立服务器上一模一样的目录，
如果使用 `-nd` 参数，那么服务器上下载的所有内容都会加到本地当前目录。
```
wget -r http://place.your.url/here
```
这个命令会按照递归的方法，下载服务器上所有的目录和文件，实质就是下载整个网站。
这个命令一定要小心使用，因为在下载的时候，被下载网站指向的所有地址同 样会被下载，
因此，如果这个网站引用了其他网站，那么被引用的网站也会被下载下来！
基于这个原因，这个参数不常用。
可以用 `-l number` 参数来指定下载的层次。例如只下载两层，那么使用`-l 2`。

要是您想制作镜像站点，那么可以使用 `-m` 参数，
例如：`wget -m http://place.your.url/here`
这时 wget 会自动判断合适的参数来制作镜像站点。
此时，wget会登录到服务器上，读入robots.txt 并按 robots.txt的规定来执行。

### 12、密码和认证
wget 可以处理利用 用户名/密码 方式限制访问的网站，可以利用两个参数：
       `--http-user=用户`                设置 http 用户名为 <用户>
       `--http-password=密码`        设置 http 密码为 <密码>
对于需要证书做认证的网站，就只能利用其他下载工具了，例如 curl

## 二、curl基本用法
```
curl http://www.linux.com
```
执行后，www.linux.com 的html就会显示在屏幕上了
Ps：由于安装linux的时候很多时候是没有安装桌面的，也意味着没有浏览器，因此这个方法也经常用于测试一台服务器是否可以到达一个网站

### 1、保存访问的网页
使用linux的重定向功能保存
```
curl http://www.linux.com >> linux.html
```
可以使用curl的内置option:-o(小写)保存网页
```
$ curl -o linux.html http://www.linux.com
```
执行完成后会显示如下界面，显示100%则表示保存成功
```
% Total    % Received % Xferd  Average Speed  Time    Time    Time  Current
                                Dload  Upload  Total  Spent    Left  Speed
100 79684    0 79684    0    0  3437k      0 --:--:-- --:--:-- --:--:-- 7781k
```
可以使用curl的内置option:-O(大写)保存网页中的文件。

要注意这里后面的 url 要具体到某个文件，不然抓不下来
```
# curl -O http://www.linux.com/hello.sh
```


### 2、测试网页返回值
```
curl -o /dev/null -s -w %{http_code} www.linux.com
```
Ps:在脚本中，这是很常见的测试网站是否正常的用法

### 3、下载文件

* 利用curl下载文件。

  使用内置option：`-o`(小写)
```
curl -o dodo1.jpg http:www.linux.com/dodo1.JPG
#使用内置option：-O（大写)
# curl -O http://www.linux.com/dodo1.JPG
```
这样就会以服务器上的名称保存文件到本地

* 循环下载

有时候下载图片可以能是前面的部分名称是一样的，就最后的尾椎名不一样
```
curl -O http://www.linux.com/dodo[1-5].JPG
```
这样就会把dodo1，dodo2，dodo3，dodo4，dodo5全部保存下来

* 下载重命名

```
curl -O http://www.linux.com/{hello,bb}/dodo[1-5].JPG
```
由于下载的hello与bb中的文件名都是dodo1，dodo2，dodo3，dodo4，dodo5。因此第二次下载的会把第一次下载的覆盖，这样就需要对文件进行重命名。
```
curl -o #1_#2.JPG http://www.linux.com/{hello,bb}/dodo[1-5].JPG
```
这样在hello/dodo1.JPG的文件下载下来就会变成hello_dodo1.JPG,其他文件依此类推，从而有效的避免了文件被覆盖

* 分块下载

有时候下载的东西会比较大，这个时候我们可以分段下载。使用内置option：-r
```
curl -r 0-100 -o dodo1_part1.JPG http://www.linux.com/dodo1.JPG
curl -r 100-200 -o dodo1_part2.JPG http://www.linux.com/dodo1.JPG
curl -r 200- -o dodo1_part3.JPG http://www.linux.com/dodo1.JPG
cat dodo1_part* > dodo1.JPG
```
这样就可以查看dodo1.JPG的内容了

* 通过ftp下载文件

curl可以通过ftp下载文件，curl提供两种从ftp中下载的语法
```
curl -O -u 用户名:密码 ftp://www.linux.com/dodo1.JPG
curl -O ftp://用户名:密码@www.linux.com/dodo1.JPG
```
* 显示下载进度条

```
curl -# -O http://www.linux.com/dodo1.JPG
```
* 不会显示下载进度信息

```
curl -s -O http://www.linux.com/dodo1.JPG
```

### 4. 断点续传
在 windows中，我们可以使用迅雷这样的软件进行断点续传。curl可以通过内置 option:`-C` 同样可以达到相同的效果
如果在下载 dodo1.JPG 的过程中突然掉线了，可以使用以下的方式续传
```
curl -C -O http://www.linux.com/dodo1.JPG
```

### 5. 上传文件
curl 不仅仅可以下载文件，还可以上传文件。通过内置 option:-T 来实现
```
curl -T dodo1.JPG -u 用户名:密码 ftp://www.linux.com/img/
```
这样就向ftp服务器上传了文件dodo1.JPG
