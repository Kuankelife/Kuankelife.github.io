---
layout: post
title: "分类器：KNN参数用法解读"
author: "Leo"
header-img: "img/yu-img/post-img/kaixinsudi1.jpg"
header-mask: 0.4
catalog: true
tags:
  - Sklearn
  - 数据科学
  - 机器学习
---


## KNN文档

KNN是一种即可用于分类又可用于回归的机器学习算法。对于给定测试样本，基于距离度量找出训练集中与其最靠近的K个训练样本，然后基于这K个“邻居”的信息来进行预测。在分类任务中可使用投票法，选择这K个样本中出现最多的类别标记作为预测结果；在回归任务中可使用平均法，将这K个样本的实值输出标记的平均值作为预测结果。当然还可以基于距离远近程度进行加权平均等方法。


**用法**：
```
class sklearn.neighbors.KNeighborsClassifier(n_neighbors=5, weights=’uniform’, algorithm=’auto’, leaf_size=30, p=2, metric=’minkowski’, metric_params=None, n_jobs=None, **kwargs)[source]
```

**参数**：

- `n_neighbors` : 整数, 可不填 (默认=5)
    - 默认邻近点的数量
    
- `weights` : 字符串或者自定义类型, 可选参数，默认="uniform")

    用于预测的权重函数。可选参数如下:
    - `uniform` : 统一的权重. 在每一个邻居区域里的点的权重都是一样的。
    - `distance` : 权重点等于他们距离的倒数。使用此函数，更近的邻居对于所预测的点的影响更大。
    - `[callable]` : 用户可以自定义一个距离函数用来计算权重，此方法接收一个距离的数组，然后返回一个相同形状并且包含权重的数组。



- `algorithm` : {‘auto’, ‘ball_tree’, ‘kd_tree’, ‘brute’}, 可选参数（默认为 'auto'）

    计算最近邻居用的算法：

     - `ball_tree`： 使用算法[BallTree](http://scikit-learn.org/stable/modules/generated/sklearn.neighbors.BallTree.html#sklearn.neighbors.BallTree)

     - `kd_tree`： 使用算法[KDTree](http://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KDTree.html#sklearn.neighbors.KDTree)

     - `brute`: 使用暴力搜索.

     - `auto`: 会基于传入[fit](http://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsClassifier.html#sklearn.neighbors.KNeighborsClassifier.fit)算法会尝试从训练数据中确定最佳方法

     注意 : 如果传入fit方法的输入是稀疏的，将会重载参数设置，直接使用暴力搜索。
     
     
- `leaf_size`:(叶子数量), 整数, 可选参数(默认为 30)

    传入BallTree或者KDTree算法的叶子数量。此参数会影响构建、查询BallTree或者KDTree的速度，以及存储BallTree或者KDTree所需要的内存大小。 此可选参数根据是否是问题所需选择性使用。


- `p`: 整数, 可选参数(默认为 2)

     用于Minkowski metric（[闵可夫斯基空间](https://zh.wikipedia.org/wiki/%E9%96%94%E8%80%83%E6%96%AF%E5%9F%BA%E6%99%82%E7%A9%BA)）的超参数。p = 1, 相当于使用[曼哈顿距离](https://zh.wikipedia.org/wiki/%E6%9B%BC%E5%93%88%E9%A0%93%E8%B7%9D%E9%9B%A2) (l1)，p = 2, 相当于使用[欧几里得距离](https://zh.wikipedia.org/wiki/%E6%AC%A7%E5%87%A0%E9%87%8C%E5%BE%97%E8%B7%9D%E7%A6%BB)(l2)  对于任何 p ，使用的是[闵可夫斯基空间](https://zh.wikipedia.org/wiki/%E9%96%94%E8%80%83%E6%96%AF%E5%9F%BA%E6%99%82%E7%A9%BA)(l_p)


- `metric`:(矩阵), 字符串或者自定义类型, 默认为 ‘minkowski’

     用于树的距离矩阵。默认为[闵可夫斯基空间](https://zh.wikipedia.org/wiki/%E9%96%94%E8%80%83%E6%96%AF%E5%9F%BA%E6%99%82%E7%A9%BA)，如果和p=2一块使用相当于使用标准欧几里得矩阵. 所有可用的矩阵列表请查询 DistanceMetric 的文档。


- `metric_params`:(矩阵参数),字符串或者自定义类型, 可选参数(默认为 None)

     给矩阵方法使用的其他的关键词参数。


- `n_jobs`: int, 可选参数(默认为 1)

     用于搜索邻近点的，可并行运行的任务数量。如果为-1, 任务数量设置为CPU核的数量，不会影响[fit](http://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsClassifier.html#sklearn.neighbors.KNeighborsClassifier.fit)方法。
     
**方法**:
```
_init__(n_neighbors=5, weights=’uniform’, algorithm=’auto’, leaf_size=30, p=2, metric=’minkowski’, metric_params=None, n_jobs=None, **kwargs)
```
- `fit(X, y)`
    - 以X为训练数据，y为目标值拟合模型
- `get_params([deep])`
    - 获取拟合器的参数
        
- `kneighbors([X, n_neighbors, return_distance])`

    找到一个点的k邻域，返回每个点的索引和到相邻点的距离
    - `n_neighbors` : 整数
    - `return_distance`:布尔值，可选。默认值为True,如果为False，则不会返回距离
    
    返回
        - `dist`:表示点的长度的数组，仅当return_distance=True时才出现
        - `ind`: 最近点的索引
      
      
- `kneighbors_graph([X, n_neighbors, mode])`
    为X中的点计算k邻域的(加权)图
    
    - `n_neighbors` : 整数
    - ` mode`:{' connectivity '， ' distance '}，可选
    
    返回矩阵类型:‘connectivity’ 将返回带1和0的连通性矩阵，‘distance’点与点之间的欧氏距离
        
- `predict(X)`：
    - 预测X的类别	


- `predict_log_proba(X)`: 
    - 预测X为各个类别的概率对数值。


- `predict_proba(X)`:
    - 预测X为各个类别的概率值。
    
- `score(X, y[, sample_weight])`
    - 返回给定测试数据的平均准确度
        - `sample_weight`:类数组，shape = [n_samples]，可选
- `set_params(**params)`
    - 设置此估计器的参数

附上[scikit-learn (sklearn) 官方文档中文版](http://sklearn.apachecn.org/#/)
