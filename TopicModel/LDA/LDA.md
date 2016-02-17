# 综述

#### Heinrich, Gregor. "Parameter estimation for text analysis." University of Leipzig, Tech. Rep (2008).
> 最好的LDA综述文章，Gibbs Sampling讲解的清楚详细，以及超参数的作用和调优。还包括了Perplexity的定义。

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

----------

# Deep Dive & Evaluation

#### Tang, Jian, et al. "Understanding the limiting factors of topic modeling via posterior contraction analysis." Proceedings of The 31st International Conference on Machine Learning. 2014.
> ICML 2014 Best Paper.
>
> 文章分析了在应用LDA模型的过程中会影响Topic效果的几个因素。采用了PMI-Score和Perplexity衡量Topic效果。

> 结论:
> 
> - 文章数量一定要够多；即便文章很长，文章数量不够多都不行；
>
> - 文章需要足够长，但不用特别长；实践中，如果文章特别长，可以对文章中的词做采样，效果也能不错；
>
> - 主题的数量很重要；当主题数量过多时，效果会恶化的很快；所以避免设置太高的主题数量；
>
> - 超参要小，beta小使得topic相关的word更加集中(~0.01)；alpha小(~0.1)，对应每个文档只关联少量的主题；


#### Wallach, Hanna M., David M. Mimno, and Andrew McCallum. "Rethinking LDA: Why priors matter." Advances in neural information processing systems. 2009.
> TODO

#### Newman, David, Edwin V. Bonilla, and Wray Buntine. "Improving topic coherence with regularized topic models." Advances in neural information processing systems. 2011.
> 包含了PMI-Score的定义。文章本身没看过。
>
> PMI-Score可以用来度量LDA模型的优劣。核心思想是，对于每个Topic排名前列的词，看看他们是否经常一起出现在同一篇文章中。
