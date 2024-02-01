# Preliminaries and the Integers

## permutation
转置，对于任意一个集合S，如果一个**一一映射**作用到这个S的结果是对S中的元素进行重排(rearrange)，那么我们称这个映射叫做集合S的**转置**。

## equivalent class
等价类，满足自反性(reflexive)、对称性(symmetric)、传递性(transitive)的一种关系，就叫做等价类。

## partition
分划，如果集合X被区分成多个区域，并且这些区域互不相交，那么就这种区分就叫做一个分划。

*remark*：分划出来的每个区域都对应一个等价类，或者换个方向想，我们可以根据某种等价关系，将集合S分成多个等价类，不同的等价类就是对应着分划之后的一块区域。所以一种分划和一种等价关系是一一对应的。根据等价类的定义可以证明。(*hint:* 分成两个方向证明，在证明一种分划对应到一种等价关系时，可以尝试直接定义出那个等价关系)

## principal of well-ordering (important!)
良序（**整数集**的一个子集如果具有一个**最小元**，那么我们称这个子集是well-ordered（良序的））原则。每个自然数集合的非空子集都是良序的。这一点非常重要，因为数学归纳法就建立在良序的基础上。

## division algorithm

### description
let a and b be integers, with $b > 0$. then there exist **unique** integers q and r such that:
$a = bq + r$ where $0 \le r < b$.

*remark*: 对于这类证明，我们要验证两方面，一是存在性，二是唯一性，这种证明套路十分常见。这个定理**异常重要**，证明思路也是非常值得借鉴的。（证明过程在手写补充笔记中有）
 
## gcd
let a and b be nonzero integers. then there exist integers r and s such that 
$$
    gcd(a, b) = ar + bs.
$$

*remark*：这个定理的证明和上一个定理类似，都用到了well-ordering principal

### corollary
let a and b be two integers that are relatively prime. then there exist integers r and s such that $ar + bs = 1$

## Euclidean algorithms
这个算法过于有名，所以很多书上都能看到，这里不再赘述，但是这个算法非常重要，是余数理论的基础。用简短的一点的话讲就是**辗转相除**

## prime numbers
- let a and b be integers and p be a prime number. if $ p | ab $, then either $p | a$ or $p | b$
- there exist an infinite number of primes

## fundamental theorem of arithmetic
let n be an integer such that $n > 1$. then
$$
    n = p_1p_2...p_k,
$$
where $p_1,...,p_k$ are primes (not necessary distinct). Furthermore, this factorization is unique; that is, if
$$
    n = q_1q_2...q_l,
$$
then $k=l$ and the $q_i's$ are just the $p_i's$ rearraned.

*remark*：这个定理的证明同样是经典类型，即存在+唯一性的证明
