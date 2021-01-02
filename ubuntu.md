# Ubuntu
### gcr server 之间进行数据传递(跳过password环节;gcr是没有密码的,所以只能以此方式进行)
1.在server A上用  
```
ssh-keygen
```
先生成id_rsa.pub文件  
2.将id_rsa.pub scp到本地(拥有连接两台gcr server权限的机器),再scp到server B上  
3.如果server B没有 authorized_keys 文件,则需要
```
mkdir ~/.ssh
chmod 700 ~/.ssh
touch ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```
如果已经有该文件,直接执行最后一步即可
### 批量kill无用的GPU进程(占用显存)
```
sudo fuser -v /dev/nvidia* |awk '{for(i=1;i<=NF;i++)print "kill -9 " $i;}' | sudo sh
```
### 多版本cuda  
1.安装:
```
wget http://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda_10.2.89_440.33.01_linux.run
sudo sh cuda_10.2.89_440.33.01_linux.run --silent --toolkit --toolkitpath=/usr/local/cuda-10.2
```
### kill未被停止的占用GPU显存的进程
https://blog.csdn.net/shanglianlm/article/details/85052773
sudo fuser -v /dev/nvidia* |awk '{for(i=1;i<=NF;i++)print "kill -9 " $i;}' | sudo sh


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
1.anaconda安装 bash脚本
```
wget https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh -O ~/anaconda.sh
sudo bash ~/anaconda.sh -b -p $HOME/anaconda3
sudo echo "export PATH=/home/v-xuche3/anaconda3/bin:$PATH">>~/.bashrc
source ~/.bashrc
conda env list
```
其中路径视具体情况进行改动  
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
