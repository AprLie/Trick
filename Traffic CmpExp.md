## ASTGCN
环境安装
```
conda create -n mx python=3.5 pip
pip install  mxnet-cu100mkl
pip install -r requirement.txt
```
传入邻接链表

###
记得在train.py和lib/util.py进行注释

## STGCN
数据格式:
csv: 格式 T*N. T=288 * 天数
邻接矩阵:
N*N

运行代码
```
# pemsd3
python main.py --num_of_vertices 358 --adj_path datasets/pemsd3/pemsd3_stgcnadj.csv --time_series_path datasets/pemsd3/pemsd3_stgcndata.csv
```
```
#pemsd7
python main.py --num_of_vertices 883 --adj_path /home/xu/project/traffic/data/PEMS07/pemsd7_stgcnadj.csv --time_series_path /home/xu/project/traffic/data/PEMS07/pemsd7_stgcndata.csv
```

## graph wavenet
### pemsd3
```
python train.py --data data/pemsd3  --adjdata data/pemsd3/pemsd3_dcrnn.pkl --gcn_bool --adjtype doubletransition --addaptadj  --randomadj --num_nodes 358
```
### pemsd7
```
python train.py --data data/pemsd7  --adjdata data/pemsd7/pemsd7_dcrnn.pkl --gcn_bool --adjtype doubletransition --addaptadj  --randomadj --num_nodes 883
```
## DCRNN
生成数据: transformer.py,更改时间,输入数据集名,输出数据集名.
生成邻接矩阵:adj_gen.py.更改点数,输入邻接关系为stgcn距离矩阵.
```
python dcrnn_train.py --config_filename=data/model/dcrnn_la.yaml
```
