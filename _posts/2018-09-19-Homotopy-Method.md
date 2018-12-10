---  

title: 同伦法（Homotopy Method）  
date: 2018-09-19  
catagries: Optimization  
tags: Algorithm Optimization Newton  

---

同伦思想：给定两个拓扑空间X和Y。考虑两个连续函数$f$和$g$，而且$f、g$是X到Y的映射。如果存在一个连续映射H：$dom H : domf \times [0,1] \rightarrow Y$，满足：
  
$$
\forall x\in X, H(x, 0) = f(x) \\
\forall x\in X, H(x, 1) = g(x)
$$  

则称在**空间Y中**$f、g$同伦；  

同伦思想结合牛顿法:  

对于目标函数$F(x)$，想要求其零解 $x^\ast$，满足  

$$F(x^\ast) = 0$$  

令映射H:  

$$
H(x, s) = sF(x) + (1 -s)F_0(x)
$$  

此时$H(x, 0) = F_0(x)$, $H(x, 1) = F(x)$，$F(x)与F_0(x)$同伦。  

这里假设$F_0(x) = F(x) - F(x_0)$，其中$x_0$为一个已知的值（任意值，起始值）。那么我们可以得到：  

$$
H(x, s) = F(x) + (s - 1)F(x_0) \\
F_0(x_0) = F(x_0)- F(x_0) = 0
$$  

对于新的函数$H(x, s)=0$，其零解$x^{\ast}$，取决于$s$的取值，这里将其记为$x^\ast(s)$。而我们想要的是$H(x, 1) =F(x)= 0$的解$x^{\ast}(1)$。已知$H(x_0, 0)$的值为$0$。  

$s \in [0, 1]$，将该区间离散化为$0 = s_0 < s_1<\dots<s_n = 1$,然后应用n次牛顿法迭代求解对应的：  

$$
H(x, s_i) = 0
$$  

每次的牛顿法的起始点为上一次求得的零解$x^\ast(s_{i - 1})$，第0次的解已知为$x^\ast(s_0 = 0) = x_0$，那么第1次牛顿法求解：  

$$
x^\ast(s_1) = 0
$$   

起始点为$x_0$。

另外，可以用该算法求解无约束且可导的convex optimization问题。因为无约束问题中convex function的全局最小值处梯度为0，当不存在解析解时，可以用Homotopy Method 结合牛顿法去求梯度的零点。该梯度的零点就是原目标函数的最小值点。
