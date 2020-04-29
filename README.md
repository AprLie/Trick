# Lab
### 等高线绘制
https://pythontic.com/visualization/charts/contour%20plot



# linux

### /mnt下的权限设置
```
sudo chown -R FAREAST.XXX *
```
### 压缩和解压文件
压缩当前目录下文件夹/文件test到test.tar.gz:
```
tar -zcvf test.tar.gz test
```
解压缩当前目录下的file.tar.gz到file:
```
tar -zxvf file.tar.gz
```
### 更改win和ubuntu的启动界面顺序（默认成为先启动win）
```
sudo mv /etc/grub.d/30_os-prober /etc/grub.d/08_os-prober
sudo update-grub
reboot
```
### 查看gpu占用情况(5s刷新一次):
```bash
watch -n 5 -d nvidia-smi
```
无进程但占用显存
```
fuser -v /dev/nvidia*
```
得到隐藏的PID后,使用
```
pmap -d PID
```
查看其运行的任务或命令,然后可
```
kill PID
```
### 新环境搭建
1.anaconda安装
2.创建anaconda环境,安装所需包
```
conda create -n tf python=3.6.5 pip numpy==1.14.3 scipy==1.1.0 scikit-learn==0.19.1 matplotlib gensim tqdm networkx cudatoolkit==10.0.130 cudnn
```
3.安装tensorflow的GPU版本
```
pip install tensorflow-gpu==1.13.1
```
### nvidia 驱动
卸载原有驱动
```
sudo apt-get install remove nvidia* --purge
```
官网下载驱动（。run文件）
添加权限
```
chmod +x NVIDIA-Linux-x86_64-440.44.run
```
参见https://blog.csdn.net/xiaowo123456/article/details/100925631

# 深度学习 训练
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

# TMUX
新建会话
```
tmux new -s session_name
```
中断会话,使会话在后台运行
```
tmux detach
prefix te d
```
恢复会话
```
tmux a # 默认进入第一个会话
tmux a -t demo # 进入到名称为demo的会话
```
关闭会话
```
tmux kill-session -t demo # 关闭demo会话
tmux kill-server # 关闭服务器，所有的会话都将关闭
```
查看会话
```
tmux ls # 不在会话中
prefix te s
```
### 滚屏(tmux似乎无滚动条功能)
```
+ 表示同时按下
ctrl + F #屏幕向下滚动一屏；
ctrl + B #屏幕向上滚动一屏；
ctrl + E #屏幕向下滚动一行；
ctrl + Y #屏幕向上滚动一行；
ctrl + D #屏幕向下滚动半屏；
ctrl + U #屏幕向上滚动半屏；
```
清空屏幕
```
ctrl + l 
```
面板功能
```
te 表示按完后再按
prefix te z #当前面板放大/再按一次后恢复

```


# mac
### 剪切文件
`command + c 选定所需文件， option + command + v 剪切到指定位置`

# tensorflow
### tf.cond
tf.cond用于tf里的tensor进行数值比较等操作,形式为 tf.cond(pred,true_fn=,false_fn=).注意:pred中进行判断的tensor的dtype与true/false_fn返回的dtype类型应该一致
### 指定GPU进行训练
1.在命令行中指定
```
CUDA_VISIBLE_DEVICES=0  python run.py   #使用GPU 0
CUDA_VISIBLE_DEVICES=0,1 python run.py  #使用GPU 0,1
```
2.在python文件中指定
```py
import os
os.environ['CUDA_VISIBLE_DEVICES'] = '0'    #使用GPU 0
os.environ['CUDA_VISIBLE_DEVICES'] = '0,1'  #使用GPU 0,1
```
3.按需增加GPU显存的使用
```
config = tf.ConfigProto()
config.gpu_options.allow_growth = True
session = tf.Session(config=config)
```
### 访问服务器上的teosorboard
Mac/linux
```
ssh -L 16006:127.0.0.1:6006 account@server.address
tensorboard --logdir="/path/to/log-directory"
```
在本地访问
http://127.0.0.1:16006/

# Vim
### 显示vim中的不可见字符,如缩进等
在命令行模式下
```
:set invlist # 显示不可见字符,^I为tab,$为回车
:set nolist  # 恢复不可见
```




