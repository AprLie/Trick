# juputer notebook
## 服务器配置使用
https://www.jianshu.com/p/8fc3cd032d3c  
1.生成配置文件
```
jupyter notebook --generate-config
```
2.生成密码
```
ipython
from notebook.auth import passwd
passwd()
```
3.复制密码后
```
vi ~/.jupyter/jupyter_notebook_config.py
c.NotebookApp.ip='*'
c.NotebookApp.password = u'sha:ce...刚才复制的那个密文'
c.NotebookApp.open_browser = False
c.NotebookApp.port = 10010
```
