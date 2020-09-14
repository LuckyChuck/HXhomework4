 Action2 Paper Reading：Slope one predictors for online rating-based collaborative filtering. Daniel Lemire and Anna Maclachlan, 2007. http://arxiv.org/abs/cs/0702144.
#  积累，总结笔记，自己的思考及idea #

答：第一次看论文，数学理论部分感觉还是有所欠缺，但是还是从论文中有一些收获。
（1）In comparison to memory-based schemes, model-based
CF algorithms are typically faster at query time though they
might have expensive learning or updating phases. Modelbased schemes can be preferable to memory-based schemes
when query speed is crucial.


与基于内存的方案相比，是基于模型的CF算法在查询时间上通常更快 尽管有昂贵的学习或更新阶段。当查询速度至关重要时。基于模型的方案优于基于内存的方案

心得：的确是，基于内存的算法当在数据量比较小的时候，是可以支持实时推荐的，但是当数据量比较大的时候，基于模型的协同过滤算法尽管在模型训练上所花费的时间比较长，但是一旦模型训练到位，推荐的速度还是十分快的。这一点又是基于内存的算法不能比拟的。所以无论是什么算法都没有完美的，都是各有利弊，还是要基于客观条件灵活的选择。


（2）Some potential drawbacks of memory-based CF include scalability and sensitivity to data sparseness. In general, schemes that rely on similarities across users cannot be precomputed for fast online queries. Another critical issue is that memory-based schemes must compute a similarity measure between users and often this requires that some minimum number of users (say, at least 100 users) have entered some minimum number of ratings (say, at least 20 ratings) including the current user.


基于内存的CF的一些潜在缺点包括可伸缩性和对数据稀疏的敏感性。一般来说，依赖于用户之间相似度的方案不能预先计算用于快速在线查询。另一个关键问题是基于内存的方案必须在用户之间计算相似性.这通常要求至少有一些用户(比如，至少100个用户)输入了包括当前用户在内的最低评级数量(比如，至少20个评级)。

心得：目前人工智能遇到的几个比较显著的问题就有数据的稀疏性，就像电影评分一样，可能众多的电影中，一个用户只对其中几个电影进行了评分，而其他的地方就成了稀疏矩阵。这对算法和模型的训练有不好的影响。所以只能是从其他地方入手，如als算法。  而且如果是user_cf的话，还是需要一定量的用户数据，无法解决冷启动的问题。


本片论文中讲述的slope_one算法，原理简单，在面对大数据量的时候，有很大的优势，而且其中其实已经包含了用户个性化和item的个性化信息，准确度在一定程度上也是很不错的。



# Thinking1	ALS都有哪些应用场景 #

答：ALS推荐基于隐语义模型，给用户对未知,未点击的商品也给一个分数。通过矩阵分解，得到用户对每个目标的预测评分，再根据评分高到低的排序对用户进行推荐。


# Thinking2	ALS进行矩阵分解的时候，为什么可以并行化处理 #
答：最大的一个核心基础就是矩阵中的每个元素都是可以独立计算的，即彼此之间并无依赖性。因此我们可以把每个元素独立出来进行计算。如果用计算机来举例，对于大小为n × n 的矩阵，加入我们有n个处理器，那么结果矩阵中的每一行，都可以用一个处理器来负责计算。



# Thinking3	梯度下降法中的批量梯度下降（BGD），随机梯度下降（SGD），和小批量梯度下降有什么区别（MBGD） #

答：
（1）批量梯度下降： 在每次更新时用所有样本，以为是遍历样本，所以可靠性最高，但是也是因为遍历，所以耗费时长高，收敛慢。

（2）随机梯度下降 每次更新时用1个样本，用1个样本来近似所有的样本
更快收敛，最终解在全局最优解附近
随机梯度下降虽然提高了计算效率，降低了计算开销，但是由于每次迭代只随机选择一个样本，因此随机性比较大，容易陷进局部最优解。

（3） mini-batch梯度下降
是一个折中的办法，选取一定数目的样本组成一个小批量样本，然后用这个小批量更新梯度，这样不仅可以减少计算成本，还可以提高算法稳定性。


# Thinking4	你阅读过和推荐系统/计算广告/预测相关的论文么？有哪些论文是你比较推荐的，可以分享到微信群中 #

答：也是刚开始看论文，action2的作业算是我第一次看推荐系统的论文，能够明显感觉到数学理论部分要求比较高，暂时还不能够完全看懂，也是希望自己能够通过学习，能够在这个领域中取得自己的收获。













