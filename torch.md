# torch
## tensor
### reshape, view, permute, transpose 
1.```view```和```reshape```:  
```view```在改变shape后,和原始的是共享同一片内存,```reshape```可能/可能不传回一份原始数据的copy  
2.```view```和```transpose```:  
```view```仅仅作用在内存地址连续的数据,即必须是contiguous(可以和```contiguous```搭配使用,如果原来是连续的,则不作操作,不连续则开辟新的内存);  
```transpose```对contiguous和non-contiguous都适用.  
3.```transpose```和```permute```:   
```transpose```仅仅可以操作两个维度,而```permute```可以操作多个维度
