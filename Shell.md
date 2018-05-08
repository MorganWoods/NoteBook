# shell 脚本相关的命令汇总

[TOC]

## apt-get  
* 常用命令 [apt-get 是 ubuntu 系统的包管理命令, 在 mac os上对应的是 brew]
```shell
apt-cache show packagename              #获取包的相关信息，如说明、大小、版本等
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

## conda

- conda 常用命令  

```shell
conda create -n py35 python=3.5  #创建虚拟环境
Source activate py35             #激活环境
conda install numpy              #conda 安装
conda install anaconda    
conda info --envs                #查看当前活动的环境
conda search python
conda install pandas=0.13.0
conda update conda
conda update ipython
conda list                       #查看当前环境下已安装的包
conda list -n python34           #查看某个指定环境的已安装包
conda search numpy               #查找package信息
# 安装package
conda install -n python34 numpy
# 如果不用-n指定环境名称，则被安装在当前活跃环境
# 也可以通过-c指定通过某个channel安装
conda update -n python34 numpy   # 更新package
conda remove -n python34 numpy   # 删除package
```



## linux 
* 常用目录  
  /boot 引导程序，内核等存放的目录  
  /sbin 超级用户可以使用的命令的目录  
  /bin 普通用户使用的命令  
  /lib 共享库目录  
  /dev 设备目录  
  /root 用户root的home目录  
  /etc 全局配置文件目录  
  /usr 用户安装目录  
  /usr/include C程序语言编译使用的头文件  
  /proc 系统内部一些信息  
  /var 经常变化目录 经常放日志文件，缓存文件  
  /tmp 临时目录 系统断电 或许目录被会清空  
  /lost+found 当系统崩溃的时候，在系统修复过程中需要恢复的文件，可能就会在这里被找到了，这个目录一般为空  
* Linux Unix  终端常用命令

```shell
cd / #切换到根目录
ls 参数 目录名 #列出文件列表
mkdir #建立新目录
cp 参数 源文件 目标文件 #拷贝文件
rm 参数 文件 #删除文件
rmdir 文件夹#删除文件夹
mv 文件 #移动文件
nano 文件名 #编辑文件
vim 文件名 #编辑文件
pwd #显示路径名
cat 文件名 #显示或链接文件
file 文件名 #显示文件类型
date #显示系统当前日期时间
cal #显示日历
time 程序文件 #统计程序执行时间
history #显示最近执行过的命令及编号
r -2 #重复执行上命令列出的第二条命令
alias #给某个命令定义别名
unalias #取消定义的别名
uname #显示操作系统相关信息 
clear #清屏
who #显示当前所有设置过的环境变量
tty #显示终端或为终端的命长
w #显示当前系统活动的总信息
```

## mac

* mac 常用文件位置

```shell
1.驱动所在位置 /Systme/Library/Extensions ；
2.桌面的位置 /User/用户名/Desktop ；
3.文件通配符为星号 *  # 用来模糊搜索文件的,主要有*或?,可以代替一个或多个真正字符.
4.在 Unix系统中是区别大小写字符的，A.txt 不等于 a.txt。根目录标志 / 不是可有可无，cd /System 表示转到跟目录下的System中，而cd System 表示转到当前目录下的 System中 。

作者：Jack_lin
链接：https://www.jianshu.com/p/d9ec00d28237
來源：简书
```

* mac 终端

```shell
defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES #在 finder 上显示路径位置
killall Finder

defaults write com.apple.screencapture location 存放位置 #改变截屏图片保存位置
killall SystemUIServer

say 'hello' #让电脑说话
sleep 10 && say "hello" #10s 后提醒我 hello

chflags hidden ~/Desktop/Hidden #隐藏文件
你也可以使用 nohidden 重新让该文件夹显示。如果你要显示全部文件，推荐大家直接使用快捷键「Shift + Command + .」即可显示全部隐藏文件。

defaults write com.apple.finder CreateDesktop -bool false ; killall Finder #关闭桌面所有图标 true 为还原


open .  #用 Finder 打开当前目录


显示所有文件：defaults write com.apple.finder AppleShowAllFiles -bool true
仅显示可见文件：defaults write com.apple.finder AppleShowAllFiles -bool false
作者：Merengues
链接：https://www.zhihu.com/question/27864961/answer/38665663
来源：知乎
```



## pip  

* pip 命令

## Vim

* vim 编辑器常用命令

```shell
'''打开文件'''
vim filename  # 打开文件
vim file1 file2 file3 #打开多个文件

'''vim 的三种模式''' 
# 命令模式 (默认, 按 Esc, 按 Ctrl+[ ,进入)  左下角显示文件名或空
# 插入模式 (按 i 进入)  左下角显示 --INSERT--  ; Esc 关闭插入模式
# 可视模式 ()左下角显示 --VISUAL--

'''退出命令''' #在命令模式下操作
:wq , :x #保存并退出
:w #保存
:q #关闭
:q! #强制退出并忽略更改
:e! #放弃所有修改,并打开原来文件

'''移动光标'''
h,j,k,l # ←,↓,→,↑ 
Ctrl f,b # 上一页, 下一页


'''编辑 (命令模式)'''
u  #撤销上一步操作 undo
Ctrl r #恢复上一步操作 redo

'''帮助'''
:help

```




