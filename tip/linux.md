# Linux 小tip整理

### inode
文件系统用inode来标记实际上的存储文件，每个inode有对应的编号。
inode中包含：文件的大小，UID，GID，读写权限，最近inode修改时间，最近内容修改时间，最近文件打开时间，文件的data放在那里等
所以打开一个文件的过程：通过文件名－》inode编号－》找到inode信息—》磁盘上的data

### 基本commmand
* passwd：修改密码
* date：查看当前时间
* cal：以日历的方式查看时间
* who：查看自己的用户状态，可以查看真正的原来的用户，不会被su干扰，类似有whoami，who am i 这两个主要是格式不一样，whoami显示的是当前的用户，如果你su之后显示的是你切换的。who am i显示的是原来的用户。
* finger：查看目前登陆有几个用户，加上用户名还可以查看用户的登录记录
* clear：清屏
* echo：输出在对于的输出流，同时可以用 1>标准输出，默认屏幕 2>标准错误输出，默认屏幕 0> 标准输入， 默认键盘
* write： 加上用户名可以发送信息
* wall： 向全部在线的用户发送消息
* talk：可以请求和在线的人聊天
* pwd：当前目录地址
* mkdir：创建目录
* rmdir：删除目录(空目录)
* touch：访问文件，修改访问时间，没有就创建
* cp：拷贝文件 -R 递归 -i 提醒
* mv：移动文件
* cat：读取文件内容
* less：也是读取文件内容
* od：8进制
* mount：挂载
* umount：取消挂载
* diskutil：查看磁盘， 加list为看全部
* ln：链接文件 ln A B ： B－》A， -s为软链接
* traceroute url：显示在到达url前，经过的route
* df：磁盘信息
* last：本用户的最近的登录时间和信息
* alias a='xxx'：把xxx的别名设置为a，简化了输入
* diff a b：显示a，b的不同
* set：显示参数列表
* du：显示磁盘的使用的空间和最后的修改时间
* shutdown：关机
* awk：通常用于文本过滤
* sort：对文件进行排序，然后输出到标准输出流
* export：设置export属性
* su：切换用户
* top：显示现在正在使用的进程的信息，从CPU占有率从高到低
* chgrp：修改文件的用户组
* groups：显示所有的用户组名
* chmod：修改文件权限
* chown：修改文件的拥有者
* w：显示登录用户和他们在做什么
* uname：显示用户信息，-a为全部
* uptime：显示当前的时间和登录用户个数
* users：显示当前的用户的信息
* cmp：比较两个文件的不同，并显示第一个不同的行号
* hostname：
* ps：当前的进程信息
* wc：显示每个文件的行数，单词数和字符数
* jobs：显示当前的任务信息
* which：定位一个命令的位置
* where：定位一个文件...的位置
* kill：杀掉进程, -9 马上杀掉
* killall：马上杀掉所有进程


### 系统目录
* /bin：所有用户的可执行文件
* /sbin：系统可执行文件
* /lib：库
* /boot：内核
* /dev：设备
* /etc：系统配置
* /home：用户目录（在Mac中为Users）
* /tmp：临时目录
* /sys：系统信息


### contab设置定时启动
现有三个备份脚本程序,其中 backup1 是在每个工作日(周一至周五)的工作时间(早 9 点至晚5 半)每半小时运行一次的增量备份程序,backup2 是在每天晚上 11 点 30 分执行的全备份程序, backup3 则是在每月 1 日和 15 日凌晨 1 点运行的程序,它的功能是将相关统计数据归档到磁带上。
文件如下
分钟， 小时， 天， 不知道， 周一到周天， 文件名
\*/30 9-17   *    *       1-5      backup1 (*/30 也可以写为 0,30) 
30     23    *    *        *       backup20      1     1,15 *        *       backup3


