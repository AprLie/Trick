# args
### 增加/更新args的attribute
https://stackoverflow.com/questions/16878315/what-is-the-right-way-to-treat-python-argparse-namespace-as-a-dictionary
```python
vars(args)['xx'] = yy
```
# logger
### 关闭logger->适用于一个trial内有多个实验设置,每个设置都开了一个新的logger,此时原先的logger没有被关闭,会一直记录
```python
handlers = logger.handlers[:]
for handler in handlers:
    handler.close()
    logger.removeHandler(handler)
```
