# 与 Github 操作相关的命令记录

[TOC]

## 修改文件 ※

```python
git add <file>  # 修改文件后运行这句,跟踪文件,可以依次跟踪多个文档,依次向后排列;添加当前仓库所有文件时直接使用 git add .
git commit -m 'some words'  #提交文件,一次性提交所有文件
git push origin master # 推送修改文件到远程仓库

git status # 查看文件状态,
```

## 常用命令查询

> https://coding.net/help/doc/git/push.html

```shell
# 创建版本库
git clone <url>                  #克隆远程版本库
git init                         #初始化本地版本库
# 修改和提交
git status                       #查看状态
git diff                         #查看变更内容
git add .                        #跟踪所有改动过的文件
git add <file>                   #跟踪指定的文件
git mv <old><new>                #文件改名
git rm<file>                     #删除文件
git rm --cached<file>            #停止跟踪文件但不删除
git commit -m "commit messages"  #提交所有更新过的文件
git commit --amend               #修改最后一次改动
# 查看提交历史
git log                    #查看提交历史
git log -p <file>          #查看指定文件的提交历史
git blame <file>           #以列表方式查看指定文件的提交历史
# 撤销
git reset --hard HEAD      #撤销工作目录中所有未提交文件的修改内容
git checkout HEAD <file>   #撤销指定的未提交文件的修改内容
git revert <commit>        #撤销指定的提交
git log --before="1 days"  #退回到之前1天的版本
# 合并
git merge <branch>        #合并指定分支到当前分支
git rebase <branch>       #衍合指定分支到当前分支
# 远程操作
git remote -v                   #查看远程版本库信息
git remote show <remote>        #查看指定远程版本库信息
git remote add <remote> <url>   #添加远程版本库
git fetch <remote>              #从远程库获取代码
git pull <remote> <branch>      #下载代码及快速合并
git push <remote> <branch>      #上传代码及快速合并
git push <remote> :<branch/tag-name>  #删除远程分支或标签
git push --tags                       #上传所有标签

# 分支与标签
$ git branch                   #显示所有本地分支
$ git checkout <branch/tag>    #切换到指定分支和标签
$ git branch <new-branch>      #创建新分支
$ git branch -d <branch>       #删除本地分支
$ git tag                      #列出所有本地标签
$ git tag <tagname>            #基于最新提交创建标签
$ git tag -d <tagname>         #删除标签

# 强制覆盖命令
git push --force

```

## 初始化 Github 仓库  
在网页中新建仓库, 
本地克隆版本库,  

```python
git clone git@github.com:freelighting/NoteBook.git
```

在本地文件夹中创建 README.md 文件,  
添加 README 文件并且提交(commit 是提交的意思 -m: --message)  

```python
git add README.md  
git commit -m  "READEME for my project." 
```

向 GitHub 推送,完成版本初始化  

```python
git push origin master
```

## 删除部分文件
先在本地删除文档,然后提交(-a: --all commit all changed files )  

```python
git rm <path> <file>
git commit -a -m "a file was deleted" 
git push origin master
```



## Gitbook

以后尝试用这gitbook 记笔记吧. 等有精力再弄.