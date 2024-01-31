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
$$
    let a and b be integers, with b > 0. then there exist unique integers q and r such that:
    a = bq + r
    where 0 < r < b.
$$


