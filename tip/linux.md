# Linux 小tip整理

### inode
文件系统用inode来标记实际上的存储文件，每个inode有对应的编号。
inode中包含：文件的大小，UID，GID，读写权限，最近inode修改时间，最近内容修改时间，最近文件打开时间，文件的data放在那里等
所以打开一个文件的过程：通过文件名－》inode编号－》找到inode信息—》磁盘上的data

