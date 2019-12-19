
# Trick
## Lab
### 等高线绘制
https://pythontic.com/visualization/charts/contour%20plot
## github
### git pull, git push每次需要输入密码：
进入项目所在文件夹，然后输入
```bash
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

## linux
### 查看gpu占用情况(5s刷新一次):
```bash
watch -n 5 -d nvidia-smi
```

## 深度学习 训练
### 如何并行化+自动化调参：
在main.py中,使用argparse,增加参数/超参数
```py
parser = argparse.ArgumentParser(description="...")
parser.add_argument('--test', type=int, default=0, help='...')
```
程序运行时使用命令行+参数/超参数，如
```bash
python main.py --test 2
```
为了并行化进行,使用multiprocessing,开进程池来实现同时运行多个程序
```py
import multiprocessing
pool = multiprocessing.Pool(processes=30)
```
批量传参:将待调参数的可选值形成list,用str转化后形成不同的字符串传给os.system
```py
test_parms = np.arange(1, 5, 0.5)
for i in range(len(test_parms)):
    token = "python main.py --test " + str(test_parms[i]) + " "
    pool.apply_async(os.system, (token,))
pool.close()
pool.join()
```



