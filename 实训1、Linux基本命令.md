## ifconfig

    用于查看IP地址，用于显示或设置网络设备
    记录ip地址方便使用远程连接工具(xshell、MobaXterm等)
    
    也是我们第一条要熟悉的命令
    
    [root@exercise1 ~]# ifconfig
    ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet 192.168.119.141  netmask 255.255.255.0  broadcast 192.168.119.255
            inet6 fe80::d223:f0d0:c686:786f  prefixlen 64  scopeid 0x20<link>
            ether 00:0c:29:51:bc:aa  txqueuelen 1000  (Ethernet)
            RX packets 1967  bytes 173443 (169.3 KiB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 1467  bytes 145537 (142.1 KiB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    
    lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
            inet 127.0.0.1  netmask 255.0.0.0
            inet6 ::1  prefixlen 128  scopeid 0x10<host>
            loop  txqueuelen 1  (Local Loopback)
            RX packets 0  bytes 0 (0.0 B)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 0  bytes 0 (0.0 B)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

ifconfig == ip a 其中ens33是网卡，lo是回环地址

    [root@exercise1 ~]# ip a
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
           valid_lft forever preferred_lft forever
        inet6 ::1/128 scope host 
           valid_lft forever preferred_lft forever
    2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
        link/ether 00:0c:29:51:bc:aa brd ff:ff:ff:ff:ff:ff
        inet 192.168.119.141/24 brd 192.168.119.255 scope global dynamic ens33
           valid_lft 1577sec preferred_lft 1577sec
        inet6 fe80::d223:f0d0:c686:786f/64 scope link 
           valid_lft forever preferred_lft forever






## 用户身份
    #与$的区别：
        #代表的是超级用户(root)
        $代表的是普通用户

​    [root@exercise1 ~]#            ###表示是 root 用户登录，管理员账号登陆
​    [root@exercise1 ~]# su - abc   ###切换到 abc 普通用户
​    [abc@exercise1 ~]$             ###表示普通用户登录


![image-20221125153752736](https://note-1308251438.cos.ap-guangzhou.myqcloud.com/typora/202211251537786.png)
    
    其中[]里面各项内容的意思
    [ root   @    exercise1   ~ ]                                       #
    [ 用户名 @    主机名      当前所在的目录(~代表的是当前用户的家目录)] 代表用户身份(管理员/普通用户)
    
    /root是root的家目录
    /home是普通用户的家目录
![image-20221125153808745](https://note-1308251438.cos.ap-guangzhou.myqcloud.com/typora/202211251538792.png)



##### 






##### 经典shell报错
    [root@exercise1 ~]# lls
    -bash: lls: 未找到命令
    [root@exercise1 ~]# cd /opt1
    -bash: cd: /opt1: 没有那个文件或目录





## 路径
    路径：分为绝对路径与相对路径
    
    绝对路径
    以正斜线“/”开头
    描述道文件位置的完整说明
    任何时候你想指定文件名的时候都可以使用
    cd /opt/aa
    
    相对路径
    不以正斜线开头
    制定相对于你的当前工作目录而言的位置
    可以使用做制定文件名的快捷方式
    相对路径：cd ../opt

## pwd
    查看当前所在的工作目录
    
    [root@exercise1 ~]# pwd
    /root


## 命令格式
    命令 [选项] [参数]

## cd
    作用：切换目录（change directory）
    语法：cd 目录
    说明：直接输入 cd 表示回到当前用户的宿主（家）目录 
    
    例子1：
    [root@exercise1 ~]# cd /etc/sysconfig/network-scripts/
    [root@exercise1 network-scripts]# cd
    [root@exercise1 ~]# cd ~


​    cd ..   表示返回到上级目录位置，也就是父目录
​    cd . 表示进入到当前用户所在的目录
​    
​    例子2：
​    [root@exercise1 ~]# cd /etc/sysconfig/network-scripts/
​    [root@exercise1 network-scripts]# cd ../   #返回上一级目录，即/etc/sysconfig
​    [root@exercise1 sysconfig]# cd ./network-scripts/   #进去当前目录下的network-scripts目录
​    [root@exercise1 network-scripts]# 
​    
​    例子3：
​    [root@exercise1 network-scripts]# cd -   #表示返回切换前的目录
​    /etc/sysconfig
​    [root@exercise1 sysconfig]# 


## ls
    作用：查看当前目录下有哪些文件（list）
    语法：ls 目录/文件 ，如果什么也不加，那么查看的是当前目录下的内容 
    常用选项：命令后面不加任何选项、-l、-a、-S、-h、-t
    
    例子1：
    -l 列出文件的详细信息，如创建者，创建时间，文件的读写权限列表等等，长列表
    [root@exercise1 ~]# ls -l
    总用量 4
    -rw-------. 1 root root 1390 1月   9 09:31 anaconda-ks.cfg

​    例子2：
​    -a 列出目录下所有的文件，包括以“ . “开头的隐藏文件
​    （linux下隐藏文件是以 . 开头的，如果存在 2 个点代表存在着父目录,1 个点表示当前目录）
​    [root@exercise1 ~]# ls -a
​    .  ..  anaconda-ks.cfg  .bash_history  .bash_logout  .bash_profile  .bashrc  .cshrc  .tcshrc

​    例子3：
​    -S 以文件的大小进行排序
​    [root@exercise1 ~]# ls -lS
​    总用量 4
​    -rw-------. 1 root root 1390 1月   9 09:31 anaconda-ks.cfg
​    drwxr-xr-x. 2 root root    6 1月   9 13:05 a


​    例子5：
​    -h 以可读性较高容量显示
​    [root@exercise1 etc]# ls -lh
​    总用量 1.1M
​    -rw-r--r--.  1 root root     16 1月   9 09:31 adjtime
​    -rw-r--r--.  1 root root   1.5K 6月   7 2013 aliases
​    -rw-r--r--.  1 root root    12K 1月   9 09:43 aliases.db
​    drwxr-xr-x.  2 root root    236 1月   9 09:29 alternatives
​    -rw-------.  1 root root    541 8月   3 2017 anacrontab
​    -rw-r--r--.  1 root root     55 3月   1 2017 asound.conf
​    drwxr-x---.  3 root root     43 1月   9 09:29 audisp


​    例子6：
​    -t 以时间反向顺序进行排序
​    [root@exercise1 etc]# ls -lt
​    总用量 1040
​    ----------.  1 root root      356 1月   9 11:20 gshadow
​    -rw-r--r--.  1 root root      449 1月   9 11:20 group
​    ----------.  1 root root      585 1月   9 11:20 shadow
​    -rw-r--r--.  1 root root      846 1月   9 11:20 passwd
​    ----------.  1 root root      707 1月   9 10:30 shadow-
​    -rw-r--r--.  1 root root      461 1月   9 10:30 group-
​    
​    ls -l == ll 
​    [root@exercise1 ~]# ls -l
​    总用量 4
​    -rw-------. 1 root root 1390 1月   9 09:31 anaconda-ks.cfg
​    [root@exercise1 ~]# ll
​    总用量 4
​    -rw-------. 1 root root 1390 1月   9 09:31 anaconda-ks.cfg
​    [root@exercise1 ~]# type ll
​    ll 是 `ls -l --color=auto' 的别名


​    





## touch
    作用：常用来创建空文件,如果文件存在，则修改这个文件的时间
    语法：touch 文件名
    
    例子1：
    创建单个文件
    [root@exercise1 ~]# cd /opt/
    [root@exercise1 opt]# ll
    总用量 0
    [root@exercise1 opt]# touch a.txt
    [root@exercise1 opt]# ll
    总用量 0
    -rw-r--r--. 1 root root 0 1月   9 13:36 a.txt
    
    例子2：
    创建多个文件
        方法一：
        [root@exercise1 opt]# ll
        总用量 0
        -rw-r--r--. 1 root root 0 1月   9 13:36 a.txt
        [root@exercise1 opt]# touch b.txt c.txt
        [root@exercise1 opt]# ll
        总用量 0
        -rw-r--r--. 1 root root 0 1月   9 13:36 a.txt
        -rw-r--r--. 1 root root 0 1月   9 13:37 b.txt
        -rw-r--r--. 1 root root 0 1月   9 13:37 c.txt
        
        方法二：
        [root@exercise1 opt]# ll
        总用量 0
        -rw-r--r--. 1 root root 0 1月   9 13:36 a.txt
        -rw-r--r--. 1 root root 0 1月   9 13:37 b.txt
        -rw-r--r--. 1 root root 0 1月   9 13:37 c.txt
        [root@exercise1 opt]# touch {1..5}
        [root@exercise1 opt]# ll
        总用量 0
        -rw-r--r--. 1 root root 0 1月   9 13:38 1
        -rw-r--r--. 1 root root 0 1月   9 13:38 2
        -rw-r--r--. 1 root root 0 1月   9 13:38 3
        -rw-r--r--. 1 root root 0 1月   9 13:38 4
        -rw-r--r--. 1 root root 0 1月   9 13:38 5
        -rw-r--r--. 1 root root 0 1月   9 13:36 a.txt
        -rw-r--r--. 1 root root 0 1月   9 13:37 b.txt
        -rw-r--r--. 1 root root 0 1月   9 13:37 c.txt
        [root@exercise1 opt]# touch {d..f}.txt
        [root@exercise1 opt]# ll
        总用量 0
        -rw-r--r--. 1 root root 0 1月   9 13:38 1
        -rw-r--r--. 1 root root 0 1月   9 13:38 2
        -rw-r--r--. 1 root root 0 1月   9 13:38 3
        -rw-r--r--. 1 root root 0 1月   9 13:38 4
        -rw-r--r--. 1 root root 0 1月   9 13:38 5
        -rw-r--r--. 1 root root 0 1月   9 13:36 a.txt
        -rw-r--r--. 1 root root 0 1月   9 13:37 b.txt
        -rw-r--r--. 1 root root 0 1月   9 13:37 c.txt
        -rw-r--r--. 1 root root 0 1月   9 13:39 d.txt
        -rw-r--r--. 1 root root 0 1月   9 13:39 e.txt
        -rw-r--r--. 1 root root 0 1月   9 13:39 f.txt
        [root@exercise1 opt]# ll
        总用量 0
        -rw-r--r--. 1 root root 0 1月   9 13:38 1
        -rw-r--r--. 1 root root 0 1月   9 13:38 2
        -rw-r--r--. 1 root root 0 1月   9 13:38 3
        -rw-r--r--. 1 root root 0 1月   9 13:38 4
        -rw-r--r--. 1 root root 0 1月   9 13:38 5
        -rw-r--r--. 1 root root 0 1月   9 13:36 a.txt
        -rw-r--r--. 1 root root 0 1月   9 13:37 b.txt
        -rw-r--r--. 1 root root 0 1月   9 13:37 c.txt
        -rw-r--r--. 1 root root 0 1月   9 13:39 d.txt
        -rw-r--r--. 1 root root 0 1月   9 13:39 e.txt
        -rw-r--r--. 1 root root 0 1月   9 13:39 f.txt
        [root@exercise1 opt]# touch 1{d..f}
        [root@exercise1 opt]# ll
        总用量 0
        -rw-r--r--. 1 root root 0 1月   9 13:38 1
        -rw-r--r--. 1 root root 0 1月   9 13:41 1d
        -rw-r--r--. 1 root root 0 1月   9 13:41 1e
        -rw-r--r--. 1 root root 0 1月   9 13:41 1f
        -rw-r--r--. 1 root root 0 1月   9 13:38 2
        -rw-r--r--. 1 root root 0 1月   9 13:38 3
        -rw-r--r--. 1 root root 0 1月   9 13:38 4
        -rw-r--r--. 1 root root 0 1月   9 13:38 5
        -rw-r--r--. 1 root root 0 1月   9 13:36 a.txt
        -rw-r--r--. 1 root root 0 1月   9 13:37 b.txt
        -rw-r--r--. 1 root root 0 1月   9 13:37 c.txt
        -rw-r--r--. 1 root root 0 1月   9 13:39 d.txt
        -rw-r--r--. 1 root root 0 1月   9 13:39 e.txt
        -rw-r--r--. 1 root root 0 1月   9 13:39 f.txt
        [root@exercise1 opt]# 
        
    例子3：
    指定路径创建
    [root@exercise1 opt]# cd
    [root@exercise1 ~]# touch /opt/11.txt
    [root@exercise1 ~]# ls /opt/
    1  11.txt  1d  1e  1f  2  3  4  5  a.txt  b.txt  c.txt  d.txt  e.txt  f.txt


​    
​    创建文件方法：touch、vi\vim、重定向、tee、cat、软连接

## mkdir
    作用：创建目录
    语法：mkdir   (选项) 文件名
    
    例子1：
    创建单个目录
    [root@exercise1 opt]# ll
    总用量 0
    -rw-r--r--. 1 root root 0 1月   9 13:38 1
    -rw-r--r--. 1 root root 0 1月   9 13:46 11.txt
    -rw-r--r--. 1 root root 0 1月   9 13:41 1d
    -rw-r--r--. 1 root root 0 1月   9 13:41 1e
    -rw-r--r--. 1 root root 0 1月   9 13:41 1f
    -rw-r--r--. 1 root root 0 1月   9 13:38 2
    -rw-r--r--. 1 root root 0 1月   9 13:38 3
    -rw-r--r--. 1 root root 0 1月   9 13:38 4
    -rw-r--r--. 1 root root 0 1月   9 13:38 5
    -rw-r--r--. 1 root root 0 1月   9 13:36 a.txt
    -rw-r--r--. 1 root root 0 1月   9 13:37 b.txt
    -rw-r--r--. 1 root root 0 1月   9 13:37 c.txt
    -rw-r--r--. 1 root root 0 1月   9 13:39 d.txt
    -rw-r--r--. 1 root root 0 1月   9 13:39 e.txt
    -rw-r--r--. 1 root root 0 1月   9 13:39 f.txt
    [root@exercise1 opt]# mkdir g
    [root@exercise1 opt]# ls
    1  11.txt  1d  1e  1f  2  3  4  5  a.txt  b.txt  c.txt  d.txt  e.txt  f.txt  g


​    
​    例子2：
​    创建多个目录
​    [root@exercise1 opt]# ls
​    1  11.txt  1d  1e  1f  2  3  4  5  a.txt  b.txt  c.txt  d.txt  e.txt  f.txt  g
​    [root@exercise1 opt]# mkdir h i
​    [root@exercise1 opt]# ls
​    1  11.txt  1d  1e  1f  2  3  4  5  a.txt  b.txt  c.txt  d.txt  e.txt  f.txt  g  h  i

​    例子3：
​    指定路径创建单个目录
​    [root@exercise1 opt]# ls
​    1  11.txt  1d  1e  1f  2  3  4  5  a.txt  b.txt  c.txt  d.txt  e.txt  f.txt  g  h  i
​    [root@exercise1 opt]# cd
​    [root@exercise1 ~]# mkdir /opt/j
​    [root@exercise1 ~]# ls /opt/
​    1  11.txt  1d  1e  1f  2  3  4  5  a.txt  b.txt  c.txt  d.txt  e.txt  f.txt  g  h  i  j
​    
​    例子4：
​    在创建一个目录的时候，如果这个目录的上一级不存在的话，要加参数-p
​    [root@exercise1 opt]# mkdir z/1.txt
​    mkdir: 无法创建目录"z/1.txt": 没有那个文件或目录
​    [root@exercise1 opt]# mkdir -p z/1.txt
​    [root@exercise1 opt]# ls
​    1  11.txt  1d  1e  1f  2  3  4  5  a.txt  b.txt  c.txt  d.txt  e.txt  f.txt  g  h  i  j  z
​    [root@exercise1 opt]# ls z
​    1.txt


## rm
    作用：可以删除一个目录中的一个或多个文件或目录，对于链接文件，只是删除整个链接文件，而原文件保持不变的
    语法：rm (选项) 处理对象
    选项：
        -f   强制删除，没有提示
        -r   删除目录，递归
    
    例子1：
        单删文件或文件夹
        [root@exercise1 opt]# ls
        1  11.txt  1d  1e  1f  2  3  4  5  a.txt  b.txt  c.txt  d.txt  e.txt  f.txt  g  h  i  j  z
        [root@exercise1 opt]# rm -f a.txt 
        [root@exercise1 opt]# ls
        1  11.txt  1d  1e  1f  2  3  4  5  b.txt  c.txt  d.txt  e.txt  f.txt  g  h  i  j  z
        
    例子2：
        文件和文件夹混合删
        [root@exercise1 opt]# rm -f b.txt g 
        [root@exercise1 opt]# ls
        1  11.txt  1d  1e  1f  2  3  4  5  c.txt  d.txt  e.txt  f.txt  h  i  j  z
        
    例子3：
        递归删除
        [root@exercise1 opt]# rm -rf z
        [root@exercise1 opt]# ls
        1  11.txt  1d  1e  1f  2  3  4  5  c.txt  d.txt  e.txt  f.txt  h  i  j
        
    例子4：
        模糊删除
        [root@exercise1 opt]# ls
        1  1d  1e  1f  2  3  4  5  c.txt  d.txt  e.txt  f.txt  i.bak  j  log  log.bak  messages
        [root@exercise1 opt]# rm -rf *.txt*
        [root@exercise1 opt]# ls
        1  1d  1e  1f  2  3  4  5  i.bak  j  log  log.bak  messages
        
    注意：用rm删除东西的时候，老林建议去到对应的目录下用相对路径去删除，防止误删


## cp
    语法：cp   源文件/目录     目录文件/目录
    选项：-R/r ：递归处理，将指定目录下的所有文件与子目录一并处理
    -p: 保持源文件的属性在拷贝的过程中,不发生变化;
    
    例子1：
    复制文件
    [root@exercise1 opt]# cp /var/log/messages /opt/
    [root@exercise1 opt]# ls
    1  11.txt  1d  1e  1f  2  3  4  5  c.txt  d.txt  e.txt  f.txt  h  i  j  messages
    
    例子2：
    复制目录
    [root@exercise1 opt]# cp -r /var/log /opt/
    [root@exercise1 opt]# ls
    1  11.txt  1d  1e  1f  2  3  4  5  c.txt  d.txt  e.txt  f.txt  h  i  j  log  messages
    
    例子3：
    复制并改名字
    [root@exercise1 opt]# cp -r /var/log /opt/log.bak
    [root@exercise1 opt]# ls
    1  11.txt  1d  1e  1f  2  3  4  5  c.txt  d.txt  e.txt  f.txt  h  i  j  log  log.bak
    
    例子4：
    一次拷贝多个文件:/etc/hostname /etc/fstab /var /tmp /root /home-->/backup 
    [root@exercise1 opt]# \cp -r /etc/hostname /etc/fstab /var/ /home/ /tmp/ /root/ /backup/
    # 前提: /backup目录必须存在; 
    # 最后一个目录,一定是目标;


## mv
    语法：mv   源文件/目录     目录文件/目录
    
    例子1：
    移动目录
    [root@exercise1 opt]# ls
    1  11.txt  1d  1e  1f  2  3  4  5  c.txt  d.txt  e.txt  f.txt  h  i  j  log  log.bak  messages
    [root@exercise1 opt]# mv h i
    [root@exercise1 opt]# ls
    1  11.txt  1d  1e  1f  2  3  4  5  c.txt  d.txt  e.txt  f.txt  i  j  log  log.bak  messages
    [root@exercise1 opt]# ls i
    h
    [root@exercise1 opt]# 
    
    例子2：
    移动文件
    [root@exercise1 opt]# mv 11.txt i
    [root@exercise1 opt]# ls
    1  1d  1e  1f  2  3  4  5  c.txt  d.txt  e.txt  f.txt  i  j  log  log.bak  messages
    [root@exercise1 opt]# ls i
    11.txt  h
    [root@exercise1 opt]# 
    
    例子3：
    移动并改名字
    [root@exercise1 opt]# ls
    1  1d  1e  1f  2  3  4  5  c.txt  d.txt  e.txt  f.txt  i  j  log  log.bak  messages
    [root@exercise1 opt]# mv i i.bak
    [root@exercise1 opt]# ls
    1  1d  1e  1f  2  3  4  5  c.txt  d.txt  e.txt  f.txt  i.bak  j  log  log.bak  messages
    
    例子4：
    一次移动多个文件
    [root@exercise1 opt]# mkdir test
    [root@exercise1 opt]# mv c.txt d.txt e.txt test
    #目录test必须在最后面，而且它前面不能再出现其他目录

## vi

```
语法：vi 文件名
按“i”键进入编辑模式
然后按“esc”键退出编辑模式
然后按：wq保存退出
```

​    

## cat
    选项：
    -n   显示行号      
    语法：cat 文件名
    作用：查看文件内容，一次显示整个文件的内容
    
    例子1：
    [root@exercise1 opt]# cat /var/log/messages
    
    例子2：
    [root@exercise1 opt]# cat /var/log/messages /opt/messages > 1   
    #文件/var/log/messages，/opt/messages合并到1


## more
    作用:以分页形式显示文件内容
    语法:more + 文件名
    说明: 按下回车刷新一行，按下空格刷新一屏，按b返回上一屏，输入 q 键退出


## less
    作用:和 more 功能一样
    语法:less +文件名
    说明: 按下回车刷新一行，按下空格刷新一屏，按b返回上一屏，输入 q 键退出


​    
## more 和 less的区别:
    1.  less可以按键盘上下方向键显示上下内容,more不能通过上下方向键控制显示，但是可以通过ctrl+B返回上一页。
    2.  less不必读整个文件，加载速度会比more更快(适用于超过1G以上文件)
    3.  less退出后shell不会留下刚显示的内容,而more退出后会在shell上留下刚显示的内容，ctrl+n可以一行行删除


​    
## head
    作用: 用于显示文件的开头的内容。在默认情况下，head 命令显示文件的头 10 行内容 
    语法:head(选项)文件名
    参数: -n 显示从文件头开始的行数
          -c<数目> 显示的字节数
    
    例子1：
    [root@exercise1 opt]# head /var/log/messages 
    Jan  9 09:43:19 exercise1 journal: Runtime journal is using 6.1M (max allowed 48.8M, trying to leave 73.2M free of 482.0M available → current limit 48.8M).
    Jan  9 09:43:19 exercise1 kernel: Initializing cgroup subsys cpuset
    Jan  9 09:43:19 exercise1 kernel: Initializing cgroup subsys cpu
    Jan  9 09:43:19 exercise1 kernel: Initializing cgroup subsys cpuacct
    Jan  9 09:43:19 exercise1 kernel: Linux version 3.10.0-693.el7.x86_64 (builder@kbuilder.dev.centos.org) (gcc version 4.8.5 20150623 (Red Hat 4.8.5-16) (GCC) ) #1 SMP Tue Aug 22 21:09:27 UTC 2017
    Jan  9 09:43:19 exercise1 kernel: Command line: BOOT_IMAGE=/vmlinuz-3.10.0-693.el7.x86_64 root=UUID=c14ecb64-e445-457e-a838-04314faa45bf ro crashkernel=auto rhgb quiet LANG=zh_CN.UTF-8
    Jan  9 09:43:19 exercise1 kernel: Disabled fast string operations
    Jan  9 09:43:19 exercise1 kernel: e820: BIOS-provided physical RAM map:
    Jan  9 09:43:19 exercise1 kernel: BIOS-e820: [mem 0x0000000000000000-0x000000000009ebff] usable
    Jan  9 09:43:19 exercise1 kernel: BIOS-e820: [mem 0x000000000009ec00-0x000000000009ffff] reserved
    [root@exercise1 opt]# 


    例子2：
    [root@exercise1 opt]# head -n 3 /var/log/messages   #显示前 3 行
    Jan  9 09:43:19 exercise1 journal: Runtime journal is using 6.1M (max allowed 48.8M, trying to leave 73.2M free of 482.0M available → current limit 48.8M).
    Jan  9 09:43:19 exercise1 kernel: Initializing cgroup subsys cpuset
    Jan  9 09:43:19 exercise1 kernel: Initializing cgroup subsys cpu
    [root@exercise1 opt]# 


​    
​    例子3：
​    [root@exercise1 opt]# head -3 /var/log/messages   #显示前 3 行
​    
​    例子4：显示文件前2个字节
​    [root@exercise1 ~]# head -c2 /opt/c.txt 
​    a:
​    [root@exercise1 ~]# 


## tail
    作用: 用于显示文件中的尾部内容。默认在屏幕上显示指定文件的末尾 10 行
    语法:tail (选项)文件名
    参数:
    -n 显示文件尾部多少行的内容(n 为数字)
    -f   动态显示数据（不关闭）,常用来查看日志
    
    例子1：
    默认查看
    [root@exercise1 opt]# tail /var/log/messages 
    Jan  9 14:50:20 exercise1 systemd: Starting Network Manager Script Dispatcher Service...
    Jan  9 14:50:20 exercise1 dbus-daemon: dbus[511]: [system] Activating via systemd: service name='org.freedesktop.nm_dispatcher' unit='dbus-org.freedesktop.nm-dispatcher.service'
    Jan  9 14:50:20 exercise1 dhclient[676]: bound to 192.168.119.141 -- renewal in 835 seconds.
    Jan  9 14:50:20 exercise1 dbus[511]: [system] Successfully activated service 'org.freedesktop.nm_dispatcher'
    Jan  9 14:50:20 exercise1 dbus-daemon: dbus[511]: [system] Successfully activated service 'org.freedesktop.nm_dispatcher'
    Jan  9 14:50:20 exercise1 systemd: Started Network Manager Script Dispatcher Service.
    Jan  9 14:50:20 exercise1 nm-dispatcher: req:1 'dhcp4-change' [ens33]: new request (3 scripts)
    Jan  9 14:50:20 exercise1 nm-dispatcher: req:1 'dhcp4-change' [ens33]: start running ordered scripts...
    Jan  9 15:01:01 exercise1 systemd: Started Session 3 of user root.
    Jan  9 15:01:01 exercise1 systemd: Starting Session 3 of user root.


​    例子2：
​    [root@exercise1 opt]# tail -n 3 /var/log/messages   #查看最后 3 行记录
​    Jan  9 15:04:15 exercise1 systemd: Started Network Manager Script Dispatcher Service.
​    Jan  9 15:04:15 exercise1 nm-dispatcher: req:1 'dhcp4-change' [ens33]: new request (3 scripts)
​    Jan  9 15:04:15 exercise1 nm-dispatcher: req:1 'dhcp4-change' [ens33]: start running ordered scripts...
​    [root@exercise1 opt]# 

​    例子3：
​    tail -f /var/log/messages   #动态显示
​    多开同机子远程终端一台使用命令tail -f /var/log/messages 另一台输入echo aaa >> /var/log/messages 在那台tail机子就会看到效果







## Linux 下快捷键
    都是用Ctrl+下面的单词 ，  ^表示 Ctrl
    ^C
    终止前台运行的程序 , 如：ping g.cn 后，想停止按下Ctrl+C 
    ^D
    退出 等价exit 
    ^L
    清屏与 clear 功能一样
    ^R
    搜索历史命令，可以利用好关键词
    ^K
    删除当前光标到后面的所有内容
    ^u
    删除当前光标到前面的所有内容
    home（^A）
    快速回到行首
    end（^E）
    快速回到行尾
    


​    
## 

## 根目录下的文件夹

文件夹绝对路径 | 英文全称 | 文件夹作用
-----|-----|-----
/bin | Binaries | 存放系统命令的目录，所有用户都可以执行。
/sbin | Super User Binaries | 保存和系统环境设置相关的命令，只有超级用户可以使用这些命令，有些命令可以允许普通用户查看
/usr | Unix Shared Resources | Unix共享资源目录，存放所有命令、库、手册页等
/usr/bin | Unix Shared Resources Binaries | 存放系统命令的目录，所有用户可以执行。这些命令和系统启动无关，单用户模式下不能执行
/usr/sbin | Superuser Binaries | 存放根文件系统不必要的系统管理命令，超级用户可执行
/dev | Devices | 存放设备文件
/etc | Editable Text Configuration Chest | 存放配置文件的地方,配置文件的目录
/opt | Optional Application Software Packages | 可选应用软件包，第三方安装的软件保存位置
/lib | Library | 存放系统程序运行所需的共享库
/proc | Processes | 虚拟文件系统，数据保存在内存中，存放当前进程信息
/root | Root | 存放root用户的相关文件,root用户的家目录。宿主目录 超级用户
/tmp | Temporary | 存放临时文件
/var | Variable | 是储存各种变化的文件，比如log等等
/home | Home | 普通用户主目录
/lost+found | Lost And Found | 存放一些系统出错的检查结果(centos6中出现)
/srv | Server | 服务数据目录
/mnt | Mount | 挂载目录。临时文件系统的安装点，默认挂载光驱和软驱的目录
/media | Media | 挂载目录。 挂载媒体设备，如软盘和光盘
/run | Run | 里面的东西是系统运行时需要的, 不能随便删除. 但是重启的时候应该抛弃. 下次系统运行时重新生成








​    

 
