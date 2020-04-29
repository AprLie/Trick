# SVM
1.面对大数据集时,SVM的效率堪忧(o(n^2)~o(n^3))之间的开销);其加速的方案:  
<1> 对数据做scale  
<2> 用bagging的方式进行集成  
<3> 用thundersvm加速(支持GPU)  
