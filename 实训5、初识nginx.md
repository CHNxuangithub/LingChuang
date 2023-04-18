

### 1.今日目标

1.使用编译安装nginx





### 2.编译安装

在linux里面，一般是服务的话，都会分成三部份，一个是配置文件，一个是日志文件，一个是主程序部份（包括源码）

到目前我们都是用yum源安装

这种安装方式非常方便 ，但有一个缺点，只要是一个服务，就是安装的配置文件必在/etc目录下，日志文件必在/var/log目录下面

因为软件已经指定了安装路径

只要不涉及服务，基本上是用编译安装，相当于自定义安装



### 3.编译安装三步骤：

1.configure ：预编译，这一步骤主要是为了检测环境与依赖是否符合软件安装与使用

2.make：编译，就是把一些源码编译成可以在liunx上运行的程序

3.make install ：安装



### 4.了解nginx

目前市场上nginx是排第一的web服务器，apache是排第二的web服务器，可查百度百科





### 5.编译安装nginx

```
[root@huali1 opt]# wget http://nginx.org/download/nginx-1.20.2.tar.gz			

[root@huali1 opt]# tar -zxvf nginx-1.20.2.tar.gz
[root@huali1 opt]# cd nginx-1.20.2
注： 在liunx里面一般都有个命令 -h   ；命令 --help 作为帮忙手册
[root@huali1 nginx-1.20.2]# ./configure --help    #查看预编译的帮忙手册，了解有哪一些选项或功能可以添加
[root@huali1 nginx-1.20.2]# ./configure \
--prefix=/usr/local/nginx \							#指定nginx安装的目录地址
--user=nginx \										#指定nginx的用户
--group=nginx 	\									#指定nginx的用户组
--sbin-path=/usr/local/nginx/nginx \				#指定nginx的启动文件地址
--conf-path=/usr/local/nginx/conf/nginx.conf \		#指定nginx的配置文件地址
--error-log-path=/var/log/nginx/nginx.log \			#指定nginx的错误日志文件地址
--http-log-path=/var/log/nginx/access.log \			#指定nginx的访问日志文件地址
--modules-path=/usr/local/nginx/modules \			#指定nginx的模块（包括官方与第三方软件支持的模块）存放目录
--with-select_module --with-poll_module --with-threads  --with-http_ssl_module --with-http_v2_module  --with-http_realip_module --with-http_image_filter_module --with-http_sub_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module  --with-http_stub_status_module --with-stream
#带with其它项为nginx开启的功能选项

完整命令
./configure --prefix=/usr/local/nginx --user=nginx --group=nginx --sbin-path=/usr/local/nginx/nginx --conf-path=/usr/local/nginx/conf/nginx.conf --error-log-path=/var/log/nginx/nginx.log --http-log-path=/var/log/nginx/access.log --modules-path=/usr/local/nginx/modules --with-select_module --with-poll_module --with-threads  --with-http_ssl_module --with-http_v2_module  --with-http_realip_module --with-http_image_filter_module --with-http_sub_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module  --with-http_stub_status_module --with-stream



./configure: error: C compiler cc is not found

[root@huali1 nginx-1.20.2]# yum install -y gcc gcc-c++

./configure: error: the HTTP rewrite module requires the PCRE library.
You can either disable the module by using --without-http_rewrite_module
option, or install the PCRE library into the system, or build the PCRE library
statically from the source with nginx by using --with-pcre=<path> option.

[root@huali1 nginx-1.20.2]# yum install -y pcre pcre-devel

./configure: error: SSL modules require the OpenSSL library.
You can either do not enable the modules, or install the OpenSSL library
into the system, or build the OpenSSL library statically from the source
with nginx by using --with-openssl=<path> option.

[root@huali1 nginx-1.20.2]# yum install -y openssl openssl-devel

./configure: error: the HTTP image filter module requires the GD library.
You can either do not enable the module or install the libraries.

[root@huali1 nginx-1.20.2]# yum install -y gd gd-devel

creating objs/Makefile						#出现这个标识，证明预编译已经成功通过

Configuration summary
  + using threads
  + using system PCRE library
  + using system OpenSSL library
  + using system zlib library

  nginx path prefix: "/usr/local/nginx"
  nginx binary file: "/usr/local/nginx/nginx"
  nginx modules path: "/usr/local/nginx/modules"
  nginx configuration prefix: "/usr/local/nginx/conf"
  nginx configuration file: "/usr/local/nginx/conf/nginx.conf"
  nginx pid file: "/usr/local/nginx/logs/nginx.pid"
  nginx error log file: "/var/log/nginx/nginx.log"
  nginx http access log file: "/var/log/nginx/access.log"
  nginx http client request body temporary files: "client_body_temp"
  nginx http proxy temporary files: "proxy_temp"
  nginx http fastcgi temporary files: "fastcgi_temp"
  nginx http uwsgi temporary files: "uwsgi_temp"
  nginx http scgi temporary files: "scgi_temp"

[root@huali1 nginx-1.20.2]# make 	#编译
[root@huali1 nginx-1.20.2]# make install 		#安装
[root@huali1 nginx-1.20.2]# cd /usr/local/nginx/
[root@huali1 nginx]# ll
总用量 8032
drwxr-xr-x 2 root root     333 6月  23 10:17 conf
drwxr-xr-x 2 root root      40 6月  23 10:17 html
drwxr-xr-x 2 root root       6 6月  23 10:17 logs
-rwxr-xr-x 1 root root 8222280 6月  23 10:17 nginx				#nginx主程序

[root@huali1 nginx]# ln -s /usr/local/nginx/nginx /usr/sbin/nginx		#生成软链接，相当windows的快捷方式，让我们																		  可以在命令行直接敲nginx以启动程序
[root@huali1 nginx]# ll /usr/sbin/nginx 
lrwxrwxrwx 1 root root 22 6月  23 10:26 /usr/sbin/nginx -> /usr/local/nginx/nginx
[root@huali1 nginx]# which nginx
/usr/sbin/nginx
[root@huali1 nginx]# nginx					#出现此错，主要是因为没有nginx的用户
nginx: [emerg] getpwnam("nginx") failed
[root@huali1 nginx]# id nginx
id: nginx: no such user
[root@huali1 nginx]# useradd nginx 
[root@huali1 nginx]# nginx				#启动nginx

```

验证是否成功启动：

方法1：

```
[root@huali1 nginx]# ps -ef |grep nginx				#查看进程命令，出现如下列显示，证明nginx已正常运行
root       8560      1  0 10:27 ?        00:00:00 nginx: master process nginx
nginx      8561   8560  0 10:27 ?        00:00:00 nginx: worker process
root       8563    840  0 10:31 pts/0    00:00:00 grep --color=auto nginx
```

方法2：

在浏览器上输入 http://服务器IP，出现如下界面则证明nginx成功运行

![image-20220623103427147](https://note-1308251438.cos.ap-guangzhou.myqcloud.com/typora/202207051830043.png)



如果出现如下界面，优先检查防火墙与seliunx是否关闭

![image-20220623103834621](https://note-1308251438.cos.ap-guangzhou.myqcloud.com/typora/202207051830993.png)

nginx家目录 为主目录下面的html目录、

```
[root@huali1 html]# cd /usr/local/nginx/html
[root@huali1 html]# >index.html 					#清空文件内容
[root@huali1 html]# cat index.html 
[root@huali1 html]# echo this is a good day >index.html
```

在浏览器刷新一下：

![image-20220623104734587](https://note-1308251438.cos.ap-guangzhou.myqcloud.com/typora/202207051830060.png)



### 6.上传源码到html目录

举例：上传坦克大战

![image-20220623110048447](https://note-1308251438.cos.ap-guangzhou.myqcloud.com/typora/202207051830009.png)

浏览器刷新一下：

![image-20220623110102325](https://note-1308251438.cos.ap-guangzhou.myqcloud.com/typora/202207051830081.png)



### 7.修改本地dns地址

路径为：C:\Windows\System32\drivers\etc\hosts

添加192.168.162.xxx  www.名字.com



作业：截图以自已名字的为域名的网页
