# 与 Github 操作相关的命令记录

## 初始化 Github 仓库  

在网页中新建仓库, 
本地克隆版本库,  
```shell
git clone git@github.com:freelighting/NoteBook.git
```
在本地文件夹中创建 README.md 文件,  
添加 README 文件并且提交,   
```shell
git add README.md  
git commit -m' "READEME for my project. # commit 是提交的意思 -m: --message " 
```  
向 GitHub 推送,完成版本初始化   
```shell
git push origin master
```
## 删除部分文件
先在本地删除文档,然后提交  
`git commit -a -m "a file was deleted" # -a: --all commit all changed files`  
`git push`
