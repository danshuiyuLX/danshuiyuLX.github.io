---  

title: Soft Thresholding算法  
data: 2018-12-06  
categories: Algorithm  
tags: Optimization Algorithm Matlab  

---  

Soft Thresholding 用于求解下面的优化问题：  

$$
x^* = \arg\min_x \frac{1}{2}\|y - x\|^2 + \lambda\|x\|_1\\
\lambda > 0 \tag{1}
$$  

其中$y$为不变量，可以看到原目标函数为凸函数，优化问题为无约束的凸优化问题，并且可以拆分成N个相互独立的关于$x_i$的子函数，同样是凸函数。因此可以单独求出每一个子函数的最优解，得到原目标函数的最优解。  

对于优化子函数$h_i(x_i) = \frac{1}{2}(y_i - x_i)^2 + \lambda |x_i| ,
\lambda>0 $，在$x_i = 0$处nondifferential。  

其subgradient为：  

$$
\partial h_i(x_i) = 
\begin{equation}
\left \{ \begin{array}{lr}
x_i - y_i + \lambda, \ \ x_i > 0 & \\
x_i - y_i - \lambda , \ \ x_i < 0 & \\
y_i - \lambda [-1, 1] , \ \ x_i = 0
\end{array}
\right.
\end{equation}
$$  

根据最优条件可以知道，当$0 \in \partial h_i(x_i)$时, $x_i$是最优解。

1.  当$y_i > \lambda$时，只有$x_i = y_i - \lambda$，满足$\partial h_i(x_i) = 0$。此时$x_i > 0$，其subgradient为:  $x_i - y_i + \lambda = y_i - \lambda - y_i + \lambda = 0$;
2.  同理当$y_i < -\lambda$时，只有$x_i = y_i + \lambda$，满足$\partial h_i(x_i) = 0$;
3.  当$-\lambda \le y_i \le \lambda$时，只有$x_i = 0$，满足$0 \in \partial h_i(x_i)$  

总结下来，最优解为：  

$$
x_i^*  = 
\begin{equation}
\left
\{
\begin{array}{lr}
y_i - \lambda\ \ ,&y_i > \lambda  \\
y_i + \lambda \ \ , & y_i < - \lambda  \\
0, & -\lambda \le y_i \le \lambda
\end{array}
\right.
\end{equation}
$$  

将上述最优解用一个算子表达，就是shrinkage operator  

$$
\tau_{\lambda}(y_i) = sign(y_i)\max(|y_i| - \lambda, 0)
$$  

原优化问题$(1)$的最优解则为：$\tau_{\lambda}(y)$  

在matlab中自带了shrinkage operator  

	x = wthresh(y, 's', lambda);
