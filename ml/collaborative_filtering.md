#### Sparse

Suppose data set is splited into 80/20

![image-20200515083707316](https://i.loli.net/2020/06/04/rkXO291wUtfgxQV.png)

![image-20200515083720095](https://i.loli.net/2020/06/04/dX4TEn1O6eIxumg.png)

sparse rate of test and the whole data

![image-20200515083828342](https://i.loli.net/2020/06/04/oNrbjdHfJyMUnKu.png)

Explicit feedback: predicting "rating"

Not a problem in Sparsy matrix

![image-20200515084557238](/Users/neil/Library/Application Support/typora-user-images/image-20200515084557238.png)



!!! Implicit feedback: recommandation "movie_id", ranking

Using Ranking Metrics

[推荐引擎初探](https://www.ibm.com/developerworks/cn/web/1103_zhaoct_recommstudy1/)

[动手实现基于协同过滤的电影推荐系统](http://fuxuemingzhu.cn/2018/06/12/MovieLens-Recommender/)

> 对于得到的rating数据，随机划分为两部分 A:B=7:3A:B=7:3，如果分别直接作为训练集和测试集是有问题的，因为BB中的user或者item是有可能在AA中没有出现过，这样会影响评估结果。 我们采用的方法是如果B数据中某个rating元素的user或item没有在A出现，则将该元素放到AA中用作训练集。最终AA和新加进来的元素共同构成训练集A1A1， BB留下的数据 B1B1 作为测试集。
>
> [ALS推荐算法学习与实践](https://iamhere1.github.io/2017/02/22/als/)

![image-20200519223027005](/Users/neil/Library/Application Support/typora-user-images/image-20200519223027005.png)



[机器学习套路--协同过滤推荐ALS](http://sharkdtu.com/posts/ml-als.html)