# Chapter 3 Concentration Inequalities

> 这里暂时跳过了第二章内容，原因是第二章讨论的是渐进分析，但是渐进分析只能讨论收敛的趋势，真正的误差反而可能因为常数项而变得很大，所以感觉不是一个特别有效的分析。后续有时间的话就补上。（其实还有个原因是渐进分析中用到的符号非常长而且难读，大家都会讨厌的，一上来就这么难绷的话，肯定就不继续看下去了，所以先不写）

我们在Chapter 1 中说到，我们当前的目标是证明我们的empirical risk 是 expected risk的一个良好近似。但是这一章内容不直接继续论证这一部分，而是先讨论一些后续论证需要用到的重要工具。

## 3.1 The big-O notation

为了后续的分析方便，我们需要给出大$O$记号的定义，为了让定义描述更加精确，我直接套用原课程notes中给出的定义。这里其实不用急着看，如果觉得记号的定义让人很头疼，可以先跳过，往下看精彩部分，我特意省略了一些正文中用到记号的部分。

> every occurrence of $O(x)$ is a placeholder for some function $f(x)$ such that for every $x$, $|f(x)|≤Cx$ for some absolute/universal constant $C$. In other words, when $O(n_1),...,O(n_k)$ occur in a statement, it means that there exist absolute constants $C_1,...,C_k > 0$ and functions $f_1,...,f_k$ satisfying $|f_i(x)|≤C_ix$ for all $x$, such that after replacing each occurrence $O(n_i)$ by $f_i(n_i)$, the statement is true. The difference from traditional “big-O” notation is that we do not need to send $n → ∞$ in order to define “big-O”. In nearly all cases, big-O notation is used to define an upper bound; then, the bound is identical if we simply substitute $Cx$ in place of $O(x)$.
>
> Note that the $x$ in our definition of big-O is a surrogate for an arbitrary variable. For instance, later on in this chapter, we will encounter the term $O(\sigma\sqrt{\log n})$. The definition above, applied with $x = \sigma\sqrt{\log n}$, yields the following conclusion: $O(σ\sqrt{\log n}) = f(σ\sqrt{\log n})$ for some function $f$ and constant $C$ such that $|f(σ\sqrt{\log n})|≤Cσ\sqrt{\log n}$ for all values that $σ\sqrt{\log n}$ can take. Lastly, for any $a,b ≥ 0$, we will let $a\lesssim b$ mean that there is some absolute constant $c > 0$ such that $a ≤cb$.

一个关键的地方在于这个big-O notation不是要求$x$趋向于正无穷，而是要求对任意$x$都能bound住，所以相对于传统的big-O notation 是一个条件更加严格的记号。

## 3.2 Chebyshev's inequality

### Theorem 3.1 (Chebyshev's inequality)

假设自变量$Z$是一个具备有限期望和方差的随机变量，那么
$$
\Pr[|Z-\mathbb{E}[Z]| \ge t] \le \frac{Var(Z)}{t^2}, \forall t \gt 0. \tag{3.1}
$$
这个定理说明了，我们的随机变量偏离均值的概率随着偏离程度增大而减小，并且衰减的程度是$1/t^2$，看起来不错，这意味着我们在某种程度上（某个概率的意义下）能保证我们的估计量离他的均值不远。但是遗憾的是这远远不够，这个衰减的速度还是太慢了，但至少我们朝我们的主题——***Concentration***迈进了一步。

## 3.3 Hoeffding‘s inequality

### Theorem 3.2 (Hoeffding‘s inequality)

我们假设有一组实值的独立同分布的随机变量$X_1, X_2, ... X_n$ ，并且有很高的概率保证$a_i \le X_i \le b_i$，令$\mu = \mathbb{E}[\bar{X}]$ 则有
$$
\Pr[|\bar{X} - \mu| \le \varepsilon] \ge 1-2\exp(\frac{-2n^2\varepsilon^2}{\Sigma_{i=1}^{n}(b_i - a_i)^2}) \tag{3.2}
$$
然后我们在独立性的假设下，可以证明出
$$
Var(\bar{X}) = \frac{1}{n^2}\Sigma_{i=1}^{n} Var(X_i) \le \frac{1}{n^2} \Sigma_{i=1}^{n}(b_i-a_i)^2 \tag{3.3}
$$
那么其实我们把$(3.2)$中的分母换成$\bar{X}$的方差是没问题的，不等式仍然会成立。不过我们这边将原来的这个分母看成是方差的一个代理，这样让不等式更紧一些。也就是说我们令$\sigma^{2}=\frac{1}{n^{2}} \sum_{i=1}^{n}\left(b_{i}-a_{i}\right)^{2}$，然后令$\varepsilon=O(\sigma\sqrt{\log n})=\sigma\sqrt{c\log n}$，代入我们的$(3.2)$，得到如下结果：
$$
\begin{align}
\operatorname*{Pr}\left[|\bar{X}-\mu|\leq\varepsilon\right]& \geq1-2\exp\left(\frac{-2\varepsilon^2}{\sigma^2}\right) & \tag{3.4} \\
&=1-2\exp(-2c\log n)& \tag{3.5} \\
&=1-2n^{-2c}& \tag{3.6} 
\end{align}
$$


观察这个式子，我们发现，估计量离均值的距离$\varepsilon$随着$n,c$增大的时候，概率衰减会很快。并且相对于之前的切比雪夫不等式，我们这里考虑的是一组独立同分布的随机变量，而且有个关键条件**很高的概率保证**$a_i \le X_i \le b_i$，事实上这个条件不容易做到，接下来我们的目标就是在抛弃这个条件的基础上，尝试找到更广泛的分布，保证他们也具备样本均值不会偏离期望太远的性质。



## 3.4 Sub-Gaussian random variables

### Definition 3.3 (Sub-Gaussian random variables)

一个随机变量$X$，具备有限的均值$\mu$，如果满足下面的条件，就说明是$\sigma$-sub-gaussian的，并且我们说他有方差代理$\sigma^2$（就是用来代替方差的啦）。
$$
\mathbb{E}\left[e^{\lambda(X-\mu)}\right]\leq e^{\sigma^2\lambda^2/2},\quad\forall\lambda\in\mathbb{R}. \tag{3.7}
$$

### remark 3.4

式$(3.7)$实际上是一个比较严格的条件，严格就严格在，他要求随机变量$X$的任意阶矩都存在且不会随阶数增长的很快。为什么这么说呢？因为我们注意到等式的左边其实类似随机变量的矩生成函数，不妨让$\mu$为$0$，那么我们对期望内部进行泰勒展开，我们就有
$$
\mathbb{E}[\exp(\lambda X)]=\mathbb{E}\left[\sum_{k=0}^\infty\frac{(\lambda X)^k}{k!}\right]=\sum_{k=0}^\infty\frac{\lambda^k}{k!}\mathbb{E}[X^k]. \tag{3.8}
$$
不难观察到，随着阶数$k$增大，随机变量的矩的增长速度要比$k!/\lambda^k$更加缓慢，才能保证每一项都是有限的，这是这个级数收敛的必要条件。

符合sub-gaussian分布的随机变量有非常不错的性质，我们可以轻松证明他们偏离自己的均值的概率随着偏离的距离增大而呈现指数级别的下降！这正如我们之前在Hoeffding’s inequality中看到的那样，并且我们这次不需要保证$a_i\le X_i \le b_i$.

### Theorem 3.5 (tail bound for sub-Gaussian random variables)

如果一个随机变量$X$具备有限的均值$\mu$是$\sigma-sub-Gaussian$的，那么就有如下不等式
$$
\Pr[|X-\mu|\geq t]\leq2\exp\left(-\frac{t^2}{2\sigma^2}\right),\quad\forall t\in\mathbb{R}. \tag{3.9}
$$
这里我们给出相应的证明

固定$t > 0$，$\forall \lambda > 0$
$$
\begin{align}
\mathrm{Pr}[X-\mu\geq t]& =\Pr[\exp(\lambda(X-\mu))\geq\exp(\lambda t)] \tag{3.10}\\
&\leq\exp(-\lambda t)\operatorname{E}[\exp(\lambda(X-\mu))]&& \begin{aligned}(\text{by Markov's inequality})\end{aligned} \tag{3.11}\\
&\begin{aligned}\leq\exp(-\lambda t)\exp(\sigma^2\lambda^2/2)\end{aligned}&& (\mathrm{by} (3.7)) \tag{3.12}\\
&=\exp(-\lambda t+\sigma^{2}\lambda^{2}/2). \tag{3.13}
\end{align}
$$
最后一步放缩就变得很自然了，因为这个$\lambda$是任意取的正数，所以不妨把$(3.13)$指数函数内部的式子看成一个二次函数，然后就很容易解得一个最大值作为上界。具体如下
$$
\Pr[X-\mu \ge t] \le \exp{(-\frac{t^2}{2\sigma^2})} \tag{3.14}
$$
现在我们的证明完成了一半，因为我们只处理了$X - \mu \ge t$ 的情况，但是目标是$|X - \mu| \ge t$. 这时候我们使用对称性，对随机变量$-X$用相同方法处理一遍（这里要把$t$代入为$-t$, 仍然令$t > 0$），就得到了
$$
\Pr[X-\mu \le -t] \le \exp{(-\frac{t^2}{2\sigma^2})} \tag{3.15}
$$
然后我们使用一下概率论中的***union bound***就很快得到了结果
$$
\Pr[|X-\mu|\geq t]\le\Pr[X-\mu\geq t]+\Pr[X-\mu\leq-t]\leq2\exp\left(-\frac{t^2}{2\sigma^2}\right). \tag{3.16}
$$

>***supplement*** - union bound
>$$
>\mathbb{P}\left(\bigcup_{i=1}^\infty A_i\right)\leq\sum_{i=1}^\infty\mathbb{P}(A_i).
>$$
>在这些事件$\left\{A_i\right\}$是概率空间中互不相交的子集，那么刚好可以取到等号，所以$(3.16)$中的第一个不等号可以改为等号，但是谁在意呢哈哈哈

### remark 3.6 (tail bound implies sub-Gaussianity)

我们刚刚得到的是从sub-Gaussian性质推导出$(3.9)$，但是实际上，如果一个随机变量满足式$(3.9)$，就意味着他是$\sigma-sub-Gaussian$的，遗憾的是这个证明比较复杂，这里就不阐述了。

### remark 3.7

这里本来有些对矩生成函数的坏话，但是我先不说，后面如果我认为有必要的话还是会回来补充

### Theorem 3.8 (sum of sub-Gaussian random variables is sub-Gaussian)

我们先阐述这个定理：如果$\left\{X_i\right\}$是具有方差代理$\left\{\sigma_i^2\right\}$的sub-gaussian 性质的随机变量集合，那么这组随机变量的和（记为$Z$）也是sub-Gaussian的，并且有方差代理$\Sigma_{i=1}^{n}\sigma_i^2$. 

为什么需要这个定理？因为我们后续的内容要做的其实是统计，这意味这我们的抽取的样本不止一个，所以我们需要有能够帮我们分析整租样本的定理。有了这个定理之后，我们应用一下刚刚学到的***theorem 3.5***，就不难得到
$$
\Pr[|Z-\mathbb{E}[Z]|\geq t]\leq2\exp\left(-\frac{t^2}{2\sum_{i=1}^n\sigma_i^2}\right) \tag{3.17}
$$
下面我们给出***theorem 3.8***的证明
$$
\begin{align}
\mathbb{E}\left[\operatorname{exp}\left\{\lambda(Z-\mathbb{E}[Z])\right\}\right]& =\mathbb{E}\left[\prod_{i=1}^n\exp\left\{\lambda(X_i-\mathbb{E}[X_i])\right\}\right] \tag{3.18}\\ 
&=\prod_{i=1}^n\mathbb{E}\left[\exp\left\{\lambda(X_i-\mathbb{E}[X_i])\right\}\right] &&\begin{aligned}\text{(by independency)}\end{aligned}\tag{3.19}\\
&\leq\prod_{i=1}^n\exp\left(\frac{\lambda^2\sigma_i^2}2\right) \tag{3.20}\\
&=\exp\left(\frac{\lambda^2\sum_{i=1}^n\sigma_i^2}{2}\right) \tag{3.21}
\end{align}
$$

### 3.4.1 examples of sub-Gaussian random variables

这里我们尝试用一些例子辅助理解sub-Gaussian的魅力，并且这些例子不是随意选取的，后续的内容也会使用到这类随机变量。

#### example 3.9 (Rademacher random variables)

>  非常重要的一类随机变量！后续会讲解Rademacher complexity，是当前广泛用来描述机器学习算法复杂度的complexity measure，其优势就在于把原问题中的随机变量转化为了简单的Rademacher random variables来处理。

首先我们给出Rademacher随机变量的定义：一个Rademacher随机变量$\epsilon$有0.5的概率取值为1,0,5的概率取值为-1。

我们可以证明$\epsilon$是$1-sub-Gaussian$的。
$$
\begin{align}
\mathbb{E}[\operatorname{exp}(\lambda\epsilon)]& =\frac12\left\{\exp(-\lambda)+\exp(\lambda)\right\} \tag{3.22}\\
&=\frac12\left\{\sum_{k=0}^\infty\frac{(-\lambda)^k}{k!}+\sum_{k=0}^\infty\frac{\lambda^k}{k!}\right\} \tag{3.23}\\
&=\sum_{k=0}^\infty\frac{\lambda^{2k}}{(2k)!}&& (\text{for odd }k, (-\lambda)^k+\lambda^k=0) \tag{3.24}\\
&\leq1+\sum_{k=1}^\infty\frac{\left(\lambda^2\right)^k}{2^kk!}&& \begin{aligned}(2^kk!\text{是}(2k)!\text{的偶数项乘积})\end{aligned} \tag{3.25}\\
&=\exp(\lambda^2/2) \tag{3.26}
\end{align}
$$

#### example 3.10 (Gaussian random variables)

如果$X$ 是具备方差$\sigma^2$的高斯型随机变量，那么$X$天然满足$(3.9)$中的取等条件，并且他的方差代理和方差相同。这也许是我们把这类随机变量称为sub-Gaussian的原因吧。

这个太容易证明了，写出高斯分布的定义就直接证完了，这里就不赘述。



#### more examples 待补充

### 3.5 Concentrations of functions of random variables

> 接下来的内容看起来会稍微有点棘手（指符号看起来比较高级），但是notes中也写的十分详尽，所以放轻松，光是只追求看懂的话还是和上面的内容一样简单。















