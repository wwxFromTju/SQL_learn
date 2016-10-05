# 结合Proxifier和shadowsocks来在Mac下全局上网

### 下载
[https://www.proxifier.com/mac\_download.htm][1]

### 激活
如果可能的话，还是希望大家使用去支持开发者
P427L-9Y552-5433E-8DSR3-58Z68

### 使用
1. 创建proxies，增加新的proxies，选择127.0.0.1，Port：1080，Type：SOCK5
2. 增加Shadowsocks的direct连接，在Rule下添加Application中Shadowsocks，Action：direct
3. 增加所有连接到刚才增加的Proxy，在Rule下修改default下Action修改为通过proxy转发即可

[1]:	https://www.proxifier.com/mac_download.htm