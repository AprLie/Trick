# Ubuntu
### 多版本cuda  
1.安装:
```
wget http://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda_10.2.89_440.33.01_linux.run
sudo sh cuda_10.2.89_440.33.01_linux.run --silent --toolkit --toolkitpath=/usr/local/cuda-10.2
```




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
