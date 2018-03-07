# 与 Github 操作相关的命令记录

## 常用命令

$ git clone <url>                  #克隆远程版本库
$ git init                         #初始化本地版本库


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
## 修改文件  

```python
git add <file>  
git commit  
git push origin master
```
