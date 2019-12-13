# Trick
## github
### git pull后如何退出GUN: 
Ctrl+X 
###初始未生成.gitignore文件,后续添加后,如何让.gitignore生效:
<p>
git rm -r --cached .
git add .
git commit -m 'add .gitignore'
</p>
## linux
###查看gpu占用情况(5s刷新一次):
watch -n 5 -d nvidia-smi
