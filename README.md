# Trick
## github
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

## linux
### 查看gpu占用情况(5s刷新一次):
```
watch -n 5 -d nvidia-smi
```
