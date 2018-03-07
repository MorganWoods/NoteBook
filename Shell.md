# shell 脚本相关

## apt-get
* 常用命令
```python
apt-cache show packagename              #获取包的相关信息，如说明、大小、版本等
apt-cache depends packagename           #了解使用依赖
apt-cache rdepends packagename          #是查看该包被哪些包依赖
apt-get install packagename             #安装包
apt-get install package=version         #指定安装版本
apt-get install packagename --reinstall #重新安装包
apt-get remove packagename --purge      #卸载程序，包括删除配置文件等
apt-get update                          #更新源,更新 /etc/apt/sources.list里的链接地址
apt-get upgrade -u                      #升级程序(不包括依赖关系改变的) -u 完整显示列表
apt-get dist-upgrade                    #升级程序(包括依赖关系改变的并且重新组织依赖关系)
apt-get clean                           #删除安装包(节约硬盘空间,下次安装需要重新下载包，软件包位置：/var/cache/apt/archives/)
apt-get autoclean                       #删除已卸载的安装包(Ubuntu14.04测试发现没起作用)
apt-get autoremove                      #卸载依赖的程序
```

* apt-get的安装位置
下载后的软件存放于 /var/cache/apt/archives
安装后软件默认存放 /usr/share
可执行文件位置    /usr/bin
lib 文件位置     /usr/lib

## linux 常用目录
• /boot 引导程序，内核等存放的目录
• /sbin 超级用户可以使用的命令的目录
• /bin 普通用户使用的命令
• /lib 共享库目录
• /dev 设备目录
• /root 用户root的home目录
• /etc 全局配置文件目录
• /usr 用户安装目录
• /usr/include C程序语言编译使用的头文件
• /proc 系统内部一些信息
• /var 经常变化目录 经常放日志文件，缓存文件
• /tmp 临时目录 系统断电 或许目录被会清空
/lost+found 当系统崩溃的时候，在系统修复过程中需要恢复的文件，可能就会在这里被找到了，这个目录一般为空
