
# Trick
## Lab
### 等高线绘制
https://pythontic.com/visualization/charts/contour%20plot
## github
### git pull, git push每次需要输入密码：
进入项目所在文件夹，然后输入
```
git config --global credential.helper store
```
### git pull后如何退出GUN: 
```
Ctrl+X 
```
### 初始未生成.gitignore文件,后续添加后,如何让.gitignore生效:
```
git rm -r --cached .
git add .
git commit -m 'add .gitignore'
```
### 更多关于.gitignore的操作：https://www.cnblogs.com/kevingrace/p/5690241.html
### 删除远程库中的某些文件夹,不改变本地的文件夹(如忘记添加忽略规则就push):
```
git pull origin master
dir
git rm -r --cached <folder_name or file_name>
git commit -m 'delete <folder_name or file_name>'
git push -u origin master
```
### git commit后想撤销commit操作:
```
git reset --soft HEAD^
```
### 本地修改后，不想保存本地文件，直接从远程pull
```
# 下载远程库最新内容，不作合并
git fetch --all   
# 把HEAD指向最新的master版本
git reset --hard origin/master
git pull
```

## linux
### 查看gpu占用情况(5s刷新一次):
```
watch -n 5 -d nvidia-smi
```
