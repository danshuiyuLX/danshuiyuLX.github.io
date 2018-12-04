---
title: Schur complement-lemma
date: 2018-12-04
categories: Convex Optimizaton
tags: lemma
---

矩阵S是一个对称矩阵可以分块为：


$$
S =\begin{bmatrix}

A&B\\
B^T &C


\end{bmatrix}
$$


其中矩阵\$A\$和矩阵$C$都是对称矩阵。那么矩阵$S$正定的充要条件为：

* $A​$为正定矩阵

* $C - B^{\mathrm{T}}A^{-1}B$是正定矩阵。

要证明$S$为正定矩阵，那必须满足：
$$
\forall x\in \mathbb{R}^n, \ \ \ g(x) = x^{\mathrm{T}}Sx > 0
$$
将$x$对应的分块为$x = (y, z)$，得到：
$$
\forall(y,z), \ \ \ g(y,z) = \begin{bmatrix}y \\ z
\end{bmatrix}^{\mathrm{T}}\begin{bmatrix}A&B\\B^{\mathrm{T}}&C\end{bmatrix}\begin{bmatrix}y\\z \end{bmatrix} = y^{\mathrm{T}}Ay +z^{\mathrm{T}}B^{\mathrm{T}}y + y^{\mathrm{T}}Bz+z^{\mathrm{T}}Cz > 0
$$
上面的问题可以等价为：
$$
\forall z, \ \ \ \min_yg(y, z) > 0
$$
也就是说无论$z$取什么值，最小化$y$后得到的函数值$g$都大于0，这其中也包括了令$g$最小的$(y,z)$；当固定了$z$的时候，$\min_yg(y, z)$，是一个无约束最小化问题，对应的最优$z$满足导数为0：
$$
\nabla_y g(y, z) = 2Bz + 2Ay = 0
$$
那么$y = -A^{-1}Bz$，因为$A$是正定矩阵，所以一定可逆（S为正定矩阵首先就得满足A正定）。将最优的$y$带回到$g$中得到：
$$
\forall z, \ \ \ z^{\mathrm{T}}(C - B^{\mathrm{T}}A^{-1}B)z > 0
$$
也就是说$C - B^{\mathrm{T}}A^{-1}B$必须是正定矩阵。



反过来如果$S$为正定矩阵，那么$A$一定是正定矩阵，且$g(x)$为凸函数（Hessian矩阵为正定）。

根据partial minimization保凸，$\min_yg(y, z)$也是一个凸函数，其对应的Hessian矩阵为$C - B^{\mathrm{T}}A^{-1}B$ 也一定是一个正定矩阵。

