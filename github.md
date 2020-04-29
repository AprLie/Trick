# github
### git pull, git push每次需要输入密码：
进入项目所在文件夹，然后输入
```bash
git config --global user.name [username]
git config --global user.email [email]
git config --global credential.helper store
```
### git pull后如何退出GUN: 
```bash
Ctrl+X 
```
### 初始未生成.gitignore文件,后续添加后,如何让.gitignore生效:
```bash
git rm -r --cached .
git add .
git commit -m 'add .gitignore'
```
### 更多关于.gitignore的操作：https://www.cnblogs.com/kevingrace/p/5690241.html
### 删除远程库中的某些文件夹,不改变本地的文件夹(如忘记添加忽略规则就push):
```bash
git pull origin master
dir
git rm -r --cached <folder_name or file_name>
git commit -m 'delete <folder_name or file_name>'
git push -u origin master
```
### git add后想撤销add:
```
git status # 查看modified file
git reset HEAD # 上一次add全部撤销
git reset HEAD ./test.py # 仅撤销单个文件
```
### git commit后想撤销commit操作:
```bash
git reset --soft HEAD^
```
### 本地修改后，不想保存本地文件，直接从远程pull
```bash
# 下载远程库最新内容，不作合并
git fetch --all   
# 把HEAD指向最新的master版本
git reset --hard origin/master
git pull
```
### 本地和服务器都改了代码，一边push后另一边无法pull，显示
```
error: Your local changes to the following files would be overwritten by merge: xxx.py Please, commit your changes or stash them before you can merge.
```
先用stash保存
```
git stash
git pull
git stash pop
```
在pop步一般会出错，如
```
Auto-merging main.py
CONFLICT (content): Merge conflict in xxx.py
```
方案：
```
git status #查看出问题的地方
```
通过vim修改代码，最后
```
git add .
```
可见 https://help.github.com/cn/github/collaborating-with-issues-and-pull-requests/resolving-a-merge-conflict-using-the-command-line
