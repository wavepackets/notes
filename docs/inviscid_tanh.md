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
> 代表速度 $U^*$ と代表長 $L^*$ で無次元化されていて、 $Re=U^* L^* / \nu^*$ はレイノルズ数 ($\nu^*$ は動粘性係数)。

この式を満たす基本流があるものとし、その速度・圧力を $(U_i, P)$ とします [基本流は時間不変だとすることが多いと思いますが、必須の条件かどうか微妙なので保留にします]。
つまり、以下が成り立つものとします。
$$\begin{align*}
& \pdv{U_i}{t} = - U_j \pdv{U_i}{x_j} - \pdv{P}{x_i} + \frac{1}{Re} \nabla^2 U_i \\
& \pdv{U_i}{x_i} = 0
\end{align*}$$

この基本流に擾乱が加わって、速度・圧力が $(U_i + u_i^\prime, P+p^\prime)$ となったとします。
すると、
$$\begin{align*}
& \cancel{\pdv{U_i}{t}} + \pdv{u_i^\prime}{t} = 
- \cancel{U_j\pdv{U_i}{x_j}} - u_j^\prime \pdv{U_i}{x_j} - U_j \pdv{u_i^\prime}{x_j} - \cancel{u_j^\prime \pdv{u_i^\prime}{x_j}} 
- \cancel{\pdv{P}{x_i}} - \pdv{p^\prime}{x_i} + \cancel{\frac{1}{Re} \nabla^2 U_i} + \frac{1}{Re} \nabla^2 u_i^\prime \\
& \cancel{\pdv{U_i}{x_i}} + \pdv{u_i^\prime}{x_i} = 0
\end{align*}$$
基本流成分のみの項は、前述の等式も成り立つので消えます。
また無限小擾乱を仮定して、擾乱成分の高次の項 $u_j^\prime \pdv{u_i^\prime}{x_j}$ は消します。



## 参考文献
1. P. Schmid and D. Henningson, "Stability and Transition in Shear FLows," Springer, 2001.
