# pip 使用

##### 更新所有的包
pip3 freeze --local | grep -v '^\-e' | cut -d = -f 1  | xargs pip3 install -U


