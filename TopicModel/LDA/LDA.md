# 综述

#### Heinrich, Gregor. "Parameter estimation for text analysis." University of Leipzig, Tech. Rep (2008).
> 最好的LDA综述文章，Gibbs Sampling讲解的非常详细，以及超参数的作用和调优。

#### LDA漫游指南
> 难得的中文的综述。
> 
> MCMC和Variational Inference的推导方法都介绍了。


#### LDA数学八卦
> 难得的中文的入门文章。
> 
> 比如，将Dirichlet分布看做是制作骰子，理解起来很形象。

----------


# 性能优化

#### Yao, Limin, David Mimno, and Andrew McCallum. "Efficient methods for topic model inference on streaming document collections." Proceedings of the 15th ACM SIGKDD international conference on Knowledge discovery and data mining. ACM, 2009.

> **Sparse-LDA.**
> 
> 优化了Gibbs Sampling的计算过程，将对词的主题的采样公式
> <img src="http://chart.googleapis.com/chart?cht=tx&chl=p(z=t|w)" style="border:none;">
> 拆解成3个不同的部分。在计算的过程中，某些部分的重复计算是可以省略的。


#### Newman, David, et al. "**Distributed algorithms for topic models.**" The Journal of Machine Learning Research 10 (2009): 1801-1828.

>**AD-LDA.**
>
>Gibbs Sampling的并行化。将数据集(dataset)切分成若干份并行计算，然后在一次迭代结束后将统计量合并更新成统一的一份。再使用这统一的一份继续并行计算。


#### Hoffman, Matthew, Francis R. Bach, and David M. Blei. "**Online learning for latent dirichlet allocation.**" advances in neural information processing systems. 2010.
> Online变分推断。速度快很多。`gensim`和`vowpal_wabbit`都用的这个方法。但是输出的Topic的质量不够好，比不上MCMC。
> 
> 首先需要了解变分推断（variational inference），就是对全量的数据做EM，不断迭代至收敛。所谓的Online，就是将数据分片，对每一片数据做EM收敛，然后update参数。
> 
> 文章中实验部分参数的设定，可以帮助我们在使用`vowpal_wabbit`的时候更有效的调节参数。


