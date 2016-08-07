# Linux 小tip整理

### inode
文件系统用inode来标记实际上的存储文件，每个inode有对应的编号。
inode中包含：文件的大小，UID，GID，读写权限，最近inode修改时间，最近内容修改时间，最近文件打开时间，文件的data放在那里等
所以打开一个文件的过程：通过文件名－》inode编号－》找到inode信息—》磁盘上的data

### 基本commmand
* passwd：修改密码
* date：查看当前时间
* cal：以日历的方式查看时间
* who：查看自己的用户状态，可以查看真正的原来的用户，不会被su干扰，类似有whoami，who am i 这两个主要是格式不一样，而且只
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
* 

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



