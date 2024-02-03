# cyclic groups

## notation
$$
    n\mathbb{Z} = \left\{..., -2n, -n, 0, n, 2n, ...\right\}
$$

## cyclic subgroups
一个子群常常可以被认为是由群中一个元素生成的，也就是说，知道那个特定的元素，就能让我们计算出这个子群中的任意元素，比如我们取集合2的所有整数次方，取二元运算为对于通常数的乘法，可以根据上一节中的第二类判据来判断这个组合构成了整数集+乘法的一个子群。而且我们发现，这个子群中的所有元素都可以依赖元素2生成，也就是有了元素2之后，再通过乘法（这个群中的二元运算）得到整个子群。

### A theorem about the cyclic group
$\text{let G be a group, and a be any element in G,}$
$\text{Then the set} <a> = \left\{a^k:k \in \mathbb{Z}\right\} \text{is a subgroup of G.}$
$\text{Furthermore, <a> is the smallest subgroup of G that contains a.}$
对于这样的子群，我们称其为**循环子群**，并且称他是由元素a**生成**的。如果一个群本身（而不是他的子群）能被一个元素生成，那么我们称这个群为**循环群**，元素a被我们称为**生成元**，并且我们定义a的**阶**为最小的**正整数**n使得$a^n = e$（e是指单位元）。如果不存在这样的n，我们记a的阶为$\infty$。

*remark*：
- 一个循环群可以有多个生成元，例如1和5都能生成$\mathbb{Z}_6$（当然此处的二元运算是关于对6求余数的加法）。
- 一个循环群中并非所有元素都是一个生成元，例如$\mathbb{Z}_6$中的2。

### every cyclic group is abelian 
我们用元素a的幂次来代表a和自己做二元运算的结果，而a的幂次和a的幂次做二元运算的结果就是将两个幂次相加，两个幂次相加的过程实际上是可以交换的，所以导致了两个分别用a的幂次来表示的元素做二元运算时是可交换的。

### every subgroup of a cyclic group is cyclic
这个定理的证明可以用division algorithm和the Principal of Well-Ordering来完成。平凡情况抛开不谈，我们假设出这个子群存在一个非单位元的元素，那么这个元素可以被写作父群的生成元（记作a）的一个幂次。然后我们立马得到这个元素的逆也存在于这个子群中，那么这两个元素至少有一个幂指数是正的，这说明子群中必然有a的正整数次的一些元素。我们值把目光放在这些a的正整数次表示的元素身上，然后利用the principal of well-ordering，得到这一系列元素中指数最小的那个（记作g）。然后我们再利用the division algorithm 来证明这个子群中的所有元素都能被表示成g的幂次，就证明了g是这个子群的生成元。

#### a corollary for $\mathbb{Z}$
整数集的子群恰好是$n\mathbb{Z}$

### a proposition about the order
$\text{let G be a cyclic group of order n and suppose that a ia a generator for G.}$ 
$\text{Then } a^k = e \text{ if and only if n divides k}$

这个定理同样可以用上面the division algorithm + the principal of well-ordering来证明。我认为这个定理很重要，因为这里体现了所谓的**循环**，当幂指数达到足够大时（也就是阶数的倍数），这个元素又变回了单位元，接着又从单位元开始新一轮的循环。

还有一点非常要紧，**就是我们会发现在一个循环中，每次幂乘得到的元素都是不同的**。想证明这一点，我们首先可以证明每次循环经历的元素都是一模一样的，也就是说这确确实实是一个循环（也就是$a^1$和$a^{n+1}$相同，$a^2$和$a^{n+2}$相同，以此类推）。这一点很容易证明。然后我们需要证明一个循环中的所有元素构成的集合就是整个循环群，这一点需要一些推导，但也比较简单（hint：两个集合相互包含）。最后根据集合中的元素不能重复，得到我们需要的结论。

### the order of a cyclic subgroup generator
$\text{let G be a cyclic group of order n and suppose that } a \in G \text{ is a generator of the group}$ 
$\text{if } b = a^k, \text{ then the order of b is n/d, where } d = gcd(k,n)$

回顾一下上文中提到的一个定理，循环群的子群都是循环群，事实上我们也可以发现取循环群中任意一个元素，都能生成一个循环子群。而关于这个子循环群生成元的阶，我们可以根据现在这个定理求出。

*remark*：
- 两个数分别除以两者的gcd，得到的结果互质，这一点在这个定理的证明中要用到
- 我们仔细想想如果想要子群的生成元的阶和父群的生成元的阶相同，那么也就是d为1，也就是k与n互质的情况。

#### corollary
$\text{the generators of } \mathbb{Z}_n \text{ are the integers r such that } 1 \le r < n \text{ and } gcd(r,n) = 1$

关于这个推论，我们可以这样理解。首先1显然是一个父群的生成元，并且我们可以立马求出他的阶为n。然后我们关注和n互质的元素，他们都能作为一个子群的生成元，而且我们根据上面的定理马上可以得出他们的阶也是n。对于阶数有限的循环群，如果子群的阶数和父群相同，意味着这两个群相同（想想为什么？）