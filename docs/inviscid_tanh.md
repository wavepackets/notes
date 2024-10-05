---
title: tanh型速度分布の非粘性線形安定性解析
layout: default
nav_order: 10
---

# tanh型速度分布の非粘性線形安定性解析


Hydrodynamic stabilityの基本的な問題の一つですが、ちょっとややこしいのでまとめてみます。

## 問題設定

{: .new-title}
> 基礎式：Navier-Stokes方程式 (非圧縮)
> 
> $$ \begin{align}
& \pdv{u_i}{t} = -u_j \pdv{u_i}{x_j} - \pdv{p}{x_i} + \frac{1}{Re} \nabla^2 u_i \\
& \pdv{u_i}{x_i} = 0
\end{align}$$
> ただし、 $u_i$ は速度 ($i=1,2,3$ をそれぞれ $x, y, z$軸方向とする)、 $p$ は圧力。
> 各値は代表速度 $U^\ast$ と代表長 $L^\ast$ で無次元化されているものとし、 $Re=U^\ast L^\ast / \nu^\ast$ はレイノルズ数 ($\nu^\ast$ は動粘性係数)。

この式を満たす基本流が存在するとします〔※基本流は時間不変だとすることが多いのですが、必須ではない気がするのでひとまず時間変化してもいいものとします〕。
つまり、その速度・圧力を $(U_i, P)$ とすると、以下が成り立ちます。
$$\begin{align*}
& \pdv{U_i}{t} = - U_j \pdv{U_i}{x_j} - \pdv{P}{x_i} + \frac{1}{Re} \nabla^2 U_i \\
& \pdv{U_i}{x_i} = 0
\end{align*}$$

この基本流に擾乱が加わって、速度・圧力が $(U_i + u_i^\prime, P+p^\prime)$ となったとします。
すると、基本流成分のみの項は前述の等式より消えて、次のようになります。
$$\begin{align*}
& \cancel{\pdv{U_i}{t}} + \pdv{u_i^\prime}{t} = -
\cancel{U_j\pdv{U_i}{x_j}} - u_j^\prime \pdv{U_i}{x_j} - U_j \pdv{u_i^\prime}{x_j} - u_j^\prime \pdv{u_i^\prime}{x_j} -
\cancel{\pdv{P}{x_i}} - \pdv{p^\prime}{x_i} + \cancel{\frac{1}{Re} \nabla^2 U_i} + \frac{1}{Re} \nabla^2 u_i^\prime \\
& \cancel{\pdv{U_i}{x_i}} + \pdv{u_i^\prime}{x_i} = 0
\end{align*}$$
これが擾乱成分の(非線形)発展方程式です。

以下、擾乱成分 $(u_i^\prime, p^\prime)$ を $(u_i, p)$ と書くことにします。
次の二つを仮定します。
1. 微小擾乱 (擾乱成分の2次以上の項は無視できるほど小さい)
2. 非粘性 ($Re \to \infty$)

すると、
{: .new-title}
> 微小擾乱の線形化された発展方程式 (非圧縮・非粘性)
> 
> $$ \begin{align}
& \pdv{u_i}{t} = - u_j \pdv{U_i}{x_j} - U_j \pdv{u_i}{x_j} - \pdv{p}{x_i} \\
& \pdv{u_i}{x_i} = 0
\end{align}$$
> ただし $U_i$ は基本流の速度、 $(u_i, p)$ は微小な擾乱速度・圧力 (2次以上の項は無視)。




## 参考文献
1. P. Schmid and D. Henningson, "Stability and Transition in Shear FLows," Springer, 2001.
